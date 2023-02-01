
<template>


    <!-- 데이터관리가 복잡해서 꼭 필요할때만 써야함. 
    {{데이터 바인딩}}은 밑에 데이터가 있어야함. ->데이터를 복붙하면 안된다. 
    변경사항 반영하려면 복잡함. 자식컴포넌트가 부모가 가지고 있는 데이터를 쓰려면 props로 데이터 전송해야함. -->
    <div class="black-bg" v-if="모달창열렸니 == true">
     <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <p>{{원룸들[누른거].price}}</p>
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