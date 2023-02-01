
<template>
  <!-- 동적인 UI 만드는법  HTML.CSS 디자인 해둠.
1.UI의 현재 상태를 데이터로 저장해둠
2. 데이터에 따라 UI가 어떻게 보일지 작성.-->
  <!--data가 true면 보여줄꺼임.  -->
  <!-- v-if="조건식" -->
  <!-- props로 자식에게 데이터 보내기 . 1.데이터보내고2.등록하고3.쓰기 
      <자식:데이터="데이터">-->

  <!-- CSS로 애니메이션 주려면 1.시작전 class명 2.애니메이션 끝난 후 class명
      3.그리고 원할때 2번 class명 부착. -->
  <!-- transition으로 감싸기, 클래스명 3개 작성.-->
  <transition name="fade">
    <!-- <div class="start" :class="{ end : 모달창열렸니}"> -->
    <Modal
      @closeModal="모달창열렸니 = false"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    ></Modal>
  </transition>
  <!-- </div> -->

  <div class="menu">
    <!-- 태그 v-for = "작명 in 몇회" -->
    <!--vue 반복문. 
      array/object 집어넣기가능 -그럼 자료안의 데이터갯수만큼반복이됨. 
      작명한 변수는 데이터안의 자료가 됨.
      :key=""의 용도 -반복문쓸때 꼭 써야함, 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀.-->
    <!-- 작명 2개까지 가능, 왼쪽변수는 array데이터 오른쪽 변수는 1씩 증가하는 정수. -->
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
  </div>
  <!-- 오브젝트.name , 오브젝트.age각각 props로 전송하는법 -->

  <!-- create 단계 ->mount단계 ->컴포넌트 생성 -> update 단계(컴포넌트안의 data변하면)
   ->unmount(컴포넌트가 삭제되면) 단계 -->

   <p>지금결제하면 {{amount}}%할인</p>
   
  <Discount v-if="showDiscount==true"></Discount>

  

  <!-- Vue라면 1.원룸들 데이터를 정렬하고 끝.  -->
  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <button @click="pricereverse">가격역순정렬</button>

  <!-- {{데이터바인딩}} : JS데이터를 HTML에 꽂아넣는 문법. -->
  <!-- 쓰는 이유 : HTML에 하드코딩해놓으면 나중에 변경어려움.
                  실시간 자동 렌더링(data를 변경하면 변경사항이 HTML에도 실시간으로 반영이됨.)  
                  자주 변할거같은 데이터들은 보관하고 HTML에 {{꽂아넣자}} -->

  <!-- 부모가 수신할땐 @작명한거="" 
  자식이 보낸 데이터는 $evnet  변수에 담겨 있음.-->
  <Card
    @openModal="
      모달창열렸니 = true;
      누른거 = i;
    "
    :원룸들="원룸들[i]"
    v-for="(작명, i) in 원룸들"
    :key="작명"
  ></Card>
  <!-- <Card :원룸들 = "원룸들[1]"></Card>
    <Card :원룸들 = "원룸들[2]"></Card>
    <Card :원룸들 = "원룸들[3]"></Card>
    <Card :원룸들 = "원룸들[4]"></Card>
    <Card :원룸들 = "원룸들[5]"></Card> -->

  <!-- <div v-for="(작명,i) in 원룸들" :key="i"> -->
  <!-- 속성태그에 바인딩은 :속성 = "데이터이름" -->
  <!-- 버튼눌렀을때 자바스크립트 실행 전통방식 onclick="" vue 방식은 @click="" -->
  <!-- <img :src="원룸들[i].image" class="room-img"> -->
  <!-- i로 반복이 돌아서 누른거에 i를 주면 됨. -->
  <!-- <h4 @click="모달창열렸니=true; 누른거 = i">{{원룸들[i].title}}</h4> -->
  <!-- <p>{{원룸들[i].price}}원</p> -->
  <!-- <button @click="신고수[0]++">허위매물신고</button>  <span>신고수 : {{신고수[0]}}</span> -->
  <!-- </div> -->
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
import data from "./assets/oneroom.js";
import Discount from "./Discount.vue";
import Modal from "./Modal.vue";
import Card from "./Card.vue";

// 함수 : function 어쩌구(){} <--입력할 코드가 길면.

// var 어레이 = [1,2,3];
// 어레이[0]

export default {
  name: "App",
  // 데이터보관함.
  data() {
    return {
      // 데이터는 Object 자료로 저장.  State 공간.
      // {자료이름 : 자료내용}
      showDiscount : true,
      원룸들오지리널 : [...data],
      오브젝트: { name: "Kim", age: 20 },
      누른거: 0,
      원룸들: data,
      모달창열렸니: false,
      메뉴들: ["Home", "Shop", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      신고수: [0, 0, 0],
      amount : 30,
    };
  },
  // 함수만들고싶으면
  // 함수안에서 데이터 쓸땐 this.데이터명
  methods: {
    increase() {
      this.신고수++;
    },
    sortBack(){
    // sort()하면 원본이 변형이됨. map(),filter()등은 원본을 보존해준다.
    // 등호로 array를 집어넣으면 왼쪽 오른쪽 값 공유해주세요 임.
    // araay/object 데이터의 각각 별개의 사본을 만들려면 [...array]
    this.원룸들 = [...this.원룸들오지리널];
    },
    priceSort() {
      this.원룸들.sort(function (a, b) {
        // 양수면 a가오른쪽 음수면a가왼쪽
        return a.price - b.price;
      });
      // [3,5,2].sort() ->sort를 붙이면 정렬이됨.
    },
    pricereverse(){
      this.원룸들.sort(function(a,b){
        return b.price - a.price;
      })
    },
    // lifecycle hook 쓰려면. mount후에 뭔가 실행하고싶으면 여기 전에는 beforemount
    // 서버에서 데이터 가져오는 코드도 lifecycle hook 안에 코드 짬.

    // x초후에 뭔가 실행하려면 setTimeout()
    // 그냥함수 vs () =>{}함수
  //   mounted(){
  //     setTimeout(()=>{
  //       this.showDiscount = false;
  //     },2000);
  //   },

    mounted(){
    setInterval(()=>{
      this.amount--;
  }, 1000);
}


   },

  // 컴포넌트 등록 하는 구간.   Discount라는이름으로 임포트한 Discount를 가져다 쓰겟다.
  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  },
};
</script>

<style>
/* 퇴장 */
.fade-leave-from {
  opacity: 0;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}
/* 등장 */
.fade-enter-from {
  /* Y축으로 이동시킴. */
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}
/* .start{
   투명도와 모든속성이 변할때
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}  */
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0, 5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
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
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
