
<template>

<!-- 동적인 UI 만드는법  HTML.CSS 디자인 해둠.
1.UI의 현재 상태를 데이터로 저장해둠
2. 데이터에 따라 UI가 어떻게 보일지 작성.-->
<!--data가 true면 보여줄꺼임.  -->
<!-- v-if="조건식" -->
<!-- props로 자식에게 데이터 보내기 . 1.데이터보내고2.등록하고3.쓰기 
      <자식:데이터="데이터">-->
  <Modal :원룸들 = "원룸들" :누른거 = "누른거" :모달창열렸니 = "모달창열렸니"></Modal>


  <div class="menu">
    <!-- 태그 v-for = "작명 in 몇회" -->
    <!--vue 반복문. 
      array/object 집어넣기가능 -그럼 자료안의 데이터갯수만큼반복이됨. 
      작명한 변수는 데이터안의 자료가 됨.
      :key=""의 용도 -반복문쓸때 꼭 써야함, 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀.-->
      <!-- 작명 2개까지 가능, 왼쪽변수는 array데이터 오른쪽 변수는 1씩 증가하는 정수. -->
    <a v-for="a in 메뉴들" :key="a">{{a}}</a>

    
    
  </div>

  <Discount></Discount>
  <!-- {{데이터바인딩}} : JS데이터를 HTML에 꽂아넣는 문법. -->
  <!-- 쓰는 이유 : HTML에 하드코딩해놓으면 나중에 변경어려움.
                  실시간 자동 렌더링(data를 변경하면 변경사항이 HTML에도 실시간으로 반영이됨.)  
                  자주 변할거같은 데이터들은 보관하고 HTML에 {{꽂아넣자}} -->
  

  <div v-for="(작명,i) in 원룸들" :key="i">
  <!-- 속성태그에 바인딩은 :속성 = "데이터이름" -->
  <!-- 버튼눌렀을때 자바스크립트 실행 전통방식 onclick="" vue 방식은 @click="" -->
    <img :src="원룸들[i].image" class="room-img">
    <!-- i로 반복이 돌아서 누른거에 i를 주면 됨. -->
    <h4 @click="모달창열렸니=true; 누른거 = i">{{원룸들[i].title}}</h4>
    <p>{{원룸들[i].price}}원</p>
    <!-- <button @click="신고수[0]++">허위매물신고</button>  <span>신고수 : {{신고수[0]}}</span> -->
  </div>
  <!-- <div> -->
  <!-- 속성태그에 바인딩은 :속성 = "데이터이름" -->
   <!-- <img :src="원룸들[1].image" class="room-img">
    <h4 @click="모달창열렸니=true">{{원룸들[1].title}}</h4>
    <p>{{원룸들[1].price}}원</p> -->
    <!-- <button @click="신고수[1]++">허위매물신고</button>  <span>신고수 : {{신고수[1]}}</span> -->
  <!-- </div> -->
  <!-- <div> -->
  <!-- 속성태그에 바인딩은 :속성 = "데이터이름" -->
  <!-- <img src="./assets/room2.jpg" class="room-img"> -->
    <!-- <h4 class="red">{{products[2]}}</h4> -->
    <!-- <p>50 만원</p> -->
    <!-- <button @click="신고수[2]++">허위매물신고</button>  <span>신고수 : {{신고수[2]}}</span> -->
  <!-- </div> -->

</template>

<script>
// import/export 문법 쓰는법
// 1.export default 변수명 , 2. import 변수명 from 그 파일 경로
// 축약해둔 컴포넌트 쓰는법 1.vue파일 import 2.등록 3.쓰기
import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';

// 함수 : function 어쩌구(){} <--입력할 코드가 길면.

// var 어레이 = [1,2,3];
// 어레이[0]

export default {
  name: 'App',
  // 데이터보관함.
  data(){
    return {
      // 데이터는 Object 자료로 저장.  State 공간.
      // {자료이름 : 자료내용}
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸','마포구원룸'],
      신고수 : [0,0,0],
    }
  },
  // 함수만들고싶으면 
  // 함수안에서 데이터 쓸땐 this.데이터명
  methods : {
    increase() {
      this.신고수 ++;
    }
  },
  // 컴포넌트 등록 하는 구간.   Discount라는이름으로 임포트한 Discount를 가져다 쓰겟다.
  components: {
    Discount : Discount,
    Modal : Modal,
  }
}
</script>

<style>
body{
  margin : 0;
}
div {
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0, 5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu{
  background: darkslateblue;
  padding : 15px;
  border-radius: 5px;
}
.menu a {
  color : white;
  padding: 10px;
}
</style>
