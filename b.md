# Vue 설치, Vue 메신저 frame 모듈화 및 동작원리

## 문서 정보
> Vue3를 설치 후 Vue 메신저 frame 모듈화 방식과 동작원리

## 작업 환경
> Visual Studio Code, Node.js version-16.13.0, Vue Cli version-4.5.15 <br>
> 주요 라이브러리 : Vue-router, Vuex, jquery

## 목차
1. [Vue-router 사용법](#1-vue-router-사용법)
2. [Vue 메신저 frame 화면 구성 모듈화 및 동작 원리](#2-Vue-메신저-frame-화면-구성-및-동작-원리)
3. [Vuex store 사용법](#3-vuex-store-사용법-및-모듈화)

## 1. Vue-router 사용법
> 메신저 frame을 설명하기에 앞서 원활한 이해를 위해 라이브러리 동작 원리를 짚고 넘어가겠습니다.

### 1-1. vue-router란?   
> Vue Router는 Vue.js 공식 플러그인으로 제공되는 라우팅 라이브러리입니다.   
> Vue에서 SPA(Single Page Application)을 구현 시, 사용자 요청 경로에 따라 해당하는 컴포넌트에 매핑하여 렌더링을 결정해주는 플러그인이 Vue Router입니다.

### 1-2. router 구현하기 
  ```javascript
      // src/router/index.js

      const routes = [
          ...

          {
            path: '/chat',
            name: 'chatList',
            component: () => import('@/views/mobile/chat.vue')
          },

          ...
      ]
  ```
  path 자리엔 호출할 URI가 오게되고, component는 본인이 작성한 View폴더의 vue 파일을 import 합니다.   
  따라서  localhost:8080/chat 을 실행하게 될 경우 @/views/mobile/chat.vue 내용이 화면에 나타나게 됩니다. 
      
  ***vue에서 @/는 src/를 나타냅니다.***
      
### 1-3. router 사용하기
  위에서 설정한 router를 views 내부의 vue에서 사용해보겠습니다.
  ```vue
      // src/App.vue
      
      <router-view/>
      <div>
        <router-link to="/">
          <i class="fa fa-home"></i>
          <span> Home </span>
        </router-link>
        
        <router-link to="/chat">
          <i class="fas fa-comments"></i>
          <span> Chat </span>
        </router-link>
      </div>
  ```
  router-link to를 통해 URI를 지정하여 해당 component를 호출하는 방식입니다. (화면 새로고침 없음)   
  현재 URI의 component를 보여주는 router-view를 통해 화면에 프레임을 나타냅니다.
  
## 2. Vue 메신저 frame 화면 구성 및 동작 원리
> 각 영역의 모듈화 및 데이터 통신 방법
  0. 디렉토리 구성   
    ![image](https://user-images.githubusercontent.com/69878816/144178001-f1f5c903-b9bd-4b7b-b203-c6fe73022be5.png)   
    ** views 폴더에는 화면에 나타날 페이지 vue 파일 **   
    ** components 폴더에는 views의 vue 파일 내부 부분(조각)들 **   
    ** 각 메뉴별로 영역을 나눠 모듈화 **
  1. 실행 화면   
    ![image](https://user-images.githubusercontent.com/69878816/144180958-f20e1db5-c4ff-4b0f-abb7-c4f0a29d7d55.png)   
    빨간색 테두리 내부 영역은 App.vue에서 위 router 사용하기처럼 링크를 걸어둔 영역입니다.   
    해당 메신저 frame의 경우 하단 메뉴를 기준으로 영역을 나눴습니다.
    
  2. 모듈화 예제 1번 Views와 components 간의 연결
  ```vue
      // src/views/mobile/Home.vue
      
      ...
      
      <div>
        <userList/>  <-- script에서 선언한 component를 태그명으로 사용 하여 component 호출  3번
      </div>
      
      <script>
        import userList from '@/components/home/userList.vue'  <-- components 내부의 vue파일(Views의 조각)을 import  1번
        
        export default {
          name : 'Home',
          
          components : {  <-- import 해온 component를 사용 가능하도록 선언  2번
            userList
          }
        }
      </script>
  ```
  위 코드는 Views 폴더 내부의 Home.vue 코드의 일부 입니다.   
  View 폴더의 vue에서 모든 기능과 화면을 구성하면 코드가 무거워지고 복잡해집니다.   
  따라서 각 영역, 기능별로 분리하여 components에 모듈화하고 Views에서 호출하여 사용합니다. (다른 Views에서 재사용 가능)   
  
  <mark> Views와 Components의 연결과 똑같이 Components와 Components 끼리도 서로 호출하고 연결이 가능합니다. </mark>
  
## 3. Vuex store 사용법 및 모듈화
> 화면 구성을 알아보았으니 js (데이터 통신)을 알아보기전 라이브러리 동작 원리를 짚고 넘어가겠습니다.

### 3-1. Vuex란
> Vue.js의 상태관리 라이브러리로 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며   의도적인 방법으로 상태를 변경 및 관리할 수 있습니다.

### 3-2. Vuex store 구조
  Vuex는 state, mutations, action, getters 4가지 형태로 관리가 되며, 관리 포인트는 store 라 불립니다.
  ![image](https://user-images.githubusercontent.com/69878816/144184192-f1546b8e-d5f3-42ff-b334-d6b0323a9248.png)

### 3-3. store의 js파일 구조
```javascript
// src/store/modules/setUser.js
  
  const setUserName = {
    namespaced: true,  // 모듈이 독립적이거나 재사용되길 원할경우 true로 설정

    state: { // 변수 선언
      userName: 'userName'
    },

    getters: {  //state의 userName을 return
      getUserName: state => state.userName
    },

    mutations: {  //state의 userName을 전달받은 payload값으로 변경 (동기)
      setUserName: (state, payload) => {
        state.userName = payload
      }
    },

    actions: {  //vue에서 dispath로 data를 받아옴 (비동기)
      acUserName: ({ commit }, payload) => {

        ...

        commit('setUserName', payload)  // 받아온 데이터를 가공하여 mutations의 setUserName으로 전달
      }
    }
  }

  export default setUserName
  
```
  위 코드 처럼 modules로 js 파일을 분리하여 작성합니다. 그리고 export로 내보냅니다.   
```javascript
  // src/store/index.js
  
  import setUserName from '@/store/modules/setUserName.js
  
  const store = createStore({
  
    ...
    
    modules : {
      setUserName : setUserName
    }
  })    
  
  ...
```
  그리고 index.js에서 받아와 modules로 설정 합니다.
  main.js의 설정은 기본적으로 되어있으므로 생략하겠습니다.
  
### 3-4. store 데이터 vue에서 사용하기
  ```vue
    <span> {{$store.state.setUserName.userName}} </span>
    
    <script>
      ...
      
      methods: {
        userName() {
          let Name = this.$store.state.setUserName.userName;
        }
      }
    
  ```
  위와 같은식으로 $store로 state, getters, commit, dispatch를 통해 데이터 및 함수 접근이 가능합니다.
## 3-5 모듈화 예제 2번 js 데이터 통신
  ```vue
    // src/components/chat/chatList.vue
    
    ...
    
    <script>
    
      ...

      methods : {
        setChatName(event) {
          const target = event.currentTarget;  <-- 내가 클릭한 DOM 요소
          const ChatRoomName = $(target)  <-- 채팅방으로 전달할 유저의 이름
            .find('.relative-name').text();
          this
            .$store.commit('setUserName/setUserName',ChatRoomName);
      }
    </script>
  ```
  위 코드를 이용해 vue의 @click을 통해 setChatName 호출합니다.   
  그리고 this.$store.commit을 통해 데이터를 전달하고 채팅방의 유저 이름을 변경합니다.
  이런 방식으로 js를 사용한 component간 데이터 전달 및 통신을 store를 통해 모듈화가 가능합니다.
  
  
  ## 참조
  1. [vue-cli youtube](https://www.youtube.com/watch?v=G6rhxMuqnhU&list=PLZzSdj89sCN0sLqrTKf2m7lXe_93C19UG)
  2. [vue-router youtube](https://www.youtube.com/watch?v=aeczJLcr8xc&list=PLZzSdj89sCN0IRcwT4lJWg_qgfBFmcF6A)
  3. [Vuex 라이브러리 youtube](https://www.youtube.com/watch?v=gf_KAs7otf4&list=PLZzSdj89sCN292abcbI3utND8pA1T1OyB)
    
  ## 수정이력
    1. 2021-12-02/김효성/초기 설정, 모듈화 및 사용 예제
  
  
