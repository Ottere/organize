# Vue 설치 및 Vue 메신저 frame 모듈화

## 문서 정보
> Vue3를 설치하고 Vue 메신저 frame 모듈화

## 작업 환경
> Visual Studio Code, Node.js version-16.13.0, Vue Cli version-4.5.15 <br>
> 주요 라이브러리 : Vue-router, Vuex, jquery

## 목차
1. Vue 설치 및 라이브러리 설치
2. Vue-router 사용법
3. Vue 메신저 frame 실행 화면 및 구성
4. 파일 구조 및 분할 방식
5. Vuex를 사용한 js 모듈화

## 1. Vue 설치 및 라이브러리 설치
> Vue3 frontend 서버를 설치 및 설정합니다. <br>
> node.js가 설치된 상황을 전제로 합니다.

  1. npm install -g @vue/cli 또는 npm install -g @vue/cli@3.x.x (version 지정)
    <p>vue의 최신 버전을 설치합니다.<p>
    
  2. vue create (사용할 프로젝트 이름)
    <p>Vue 프로젝트 디렉토리를 생성합니다.<p>
    - Vue-Cli 프로젝트 설정   
    ![Vue-Cli 설정](https://user-images.githubusercontent.com/69878816/144156456-7e5b3345-0b54-4aba-a7e9-20b703fd385d.png)   
    순서대로 Vue2, Vue3, 커스텀으로 사용할지 결정합니다. 3번째 메뉴를 사용합니다.   
    ![image](https://user-images.githubusercontent.com/69878816/144160505-3adc8532-2972-4aba-ae84-30ff1fcb838e.png)   
    이후 설정은 위 사진처럼 지정합니다.   
    - 설정 이후 디렉토리 구성   
    ![image](https://user-images.githubusercontent.com/69878816/144160919-07036663-12e7-477c-a8cb-e56b1ca0c46f.png)
        
  3. Vue frontend 서버 실행 및 실행화면   
    - cd (프로젝트 이름)   
    - npm run serve   
    ![image](https://user-images.githubusercontent.com/69878816/144161596-835e98d7-7d19-494d-9c15-917c15583b9a.png)

  4. Vue 메신저 frame 사용 주요 라이브러리 목록 및 설치   
    - vuex (커스텀 설정에서 자동 설치됨), jquery, vue-router (커스텀 설정에서 자동 설치됨)   
    - npm install --save jquery

## 2. Vue-router 사용법
> 메신저 frame을 설명하기에 앞서 원활한 이해를 위해 라이브러리 동작 원리를 짚고 넘어가겠습니다.

### 2-1. vue-router란?   
> Vue Router는 Vue.js 공식 플러그인으로 제공되는 라우팅 라이브러리입니다.   
> Vue에서 SPA(Single Page Application)을 구현 시, 사용자 요청 경로에 따라 해당하는 컴포넌트에 매핑하여 렌더링을 결정해주는 플러그인이 Vue Router입니다.

### 2-2. router 구현하기
  router 경로 설정 파일의 경로는 src/router/index.js 입니다.   
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
      
### 2-3. router 사용하기
  위에서 설정한 router를 views 내부의 vue에서 사용해보겠습니다.
  ```vue
      // src/App.vue
      
      <router-view/>
      <div>
        <router-link to="/"><i class="fa fa-home"></i><span>Home</span></router-link>
        <router-link to="/chat"><i class="fas fa-comments"></i><span>Chat</span></router-link>
      </div>
  ```
  router-link to를 통해 URI를 지정하여 해당 component를 호출하는 방식입니다. (화면 새로고침 없음)   
  현재 URI의 component를 보여주는 router-view를 통해 화면에 프레임을 나타냅니다.
  
## 3. Vue 메신저 frame 실행 화면 및 구성
> 각 영역의 모듈화 및 데이터 통신 방법
  0. 디렉토리 구성   
    ![image](https://user-images.githubusercontent.com/69878816/144178001-f1f5c903-b9bd-4b7b-b203-c6fe73022be5.png)

  1. Home 화면   
    ![image](https://user-images.githubusercontent.com/69878816/144177332-c5dc8132-0897-4fd5-8bff-a8e36e1aa4b7.png)   
    빨간색 테두리 내부 영역은 App.vue에서 위 router 사용하기처럼 링크를 걸어둔 영역입니다.   
    위에 부분은 src/views/mobile/Home.vue 파일을 불러온 영역입니다.   
  ```vue
      // src/views/mobile/Home.vue
      
      ...
      
      <div>
        <userList/>
      </div>
      
      <script>
        import userList from '@/components/home/userList.vue'
        
        export default {
          name : 'Home',
          
          components : {
            userList
          }
        }
      </script>
  ```
