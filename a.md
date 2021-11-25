# Vuex를 이용한 Vue 모듈화

## 문서 정보
> Vue 프로젝트를 Vuex를 통한 모듈화<br>
> https://kdydesign.github.io/2019/05/09/vuex-tutorial/

## 목차 
1. Vuex란
2. Vuex의 구조
3. Vuex 예제

##  1. Vuex란
> Vue.js의 상태관리 라이브러리로 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 의도적인 방법으로 상태를 변경 및 관리할 수 있다.
> Vuex는 기존 Flux의 아키텍처를 따라가고 있고 React로 본다면 Redux와 비교 대상으로 볼 수 있다.

## 2. Vuex 구조
> Vuex는 state, mutations, action, getters 4가지 형태로 관리가 되며, 이때 이 관리 포인트는 store 패턴을 사용하고 통상 store라고 불린다.
  1. ### store
    전역변수
    
  2. ### state
    값을 저장하는 객체
    
  3. ### mutations
    state의 값 변경하는 함수, setter
    
  4. ### actions
    mutations에 값 보내는 함수
    
  5. ### getters
    state의 값 반환하는 함수, computed

    
