
<template>


    <!-- 데이터관리가 복잡해서 꼭 필요할때만 써야함. 
    {{데이터 바인딩}}은 밑에 데이터가 있어야함. ->데이터를 복붙하면 안된다. 
    변경사항 반영하려면 복잡함. 자식컴포넌트가 부모가 가지고 있는 데이터를 쓰려면 props로 데이터 전송해야함. -->
    <div class="black-bg" v-if="모달창열렸니 == true">
     <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <!-- input에 입력한 값 알아내기 
      축약 버전 v-model="데이터이름" -->
      <!-- <input @input="month = $event.target.value"> 축약버전 -->
      <input v-model="month">
      <p> {{month}}개월선택함 : {{원룸들[누른거].price *month}}</p>
      <!-- 부모의 데이터 수정 customevent
      1. 부모에게 수정좀 해달라고 메세지 보냄. 2.부모는 메세지오면 데이터 수정해줌 -->
      <button @click="$emit('closeModal')">닫기</button>
      <Discount></Discount>
      <!-- props는 read-only임 받아온거 수정하면 안됨. -->
      <!-- <button type="button" @click="모달창열렸니=false">닫기</button> -->

      </div>
  </div>


</template>

<script>
export default {
//eslint-disable-next-line
    name : 'Modal',
    // 유저가 <input>에 입력한 값 데이터로 저장
    data(){
        return {
            // 문자는 초기값 문자로.
            month : 1,
            date : 123
        }
    },
    watch : {
        // 데이터를 감시하려면 watch:{감시할데이터(){}}
        // month데이터가 변할때마다 watch도 실행이됨. 경고문띄우기
        // a:변경전 데이터 b:변경 후 데이터.
        month(a){
            if(a>=13){
                alert('13이상 입력하지 마세요')
            }
            //isNaN 숫자면 false 글자면 true
            else if(isNaN(a)==true) {
                alert('숫자만 입력해주세요')
            }
        },
    },
    // 자식은 props로 받은거 등록 props:{데이터이름:자료형이름}
    props: {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,

    }

}
</script>

<style>

</style>