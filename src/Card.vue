<template>
    <div>
    <img :src="원룸들.image" class="room-img">
    <!-- $어쩌구는 Vue만의 특별한 변수. $emit():부모에게 메세지 보낼떄
    $emit('작명',데이터)-->
    <h4 @click="$emit('openModal',원룸들.title)">{{원룸들.title}}</h4>
    <p>{{원룸들.price}}원</p>
  </div>
</template>

<script>
export default {
    // props로 보낸 데이터는 수정 금지. App.vue에 있는 데이터 수정하고 싶으면 custom event
   //eslint-disable-next-line
   name : 'Card',
    props: {
        원룸들 : Object,

    },
    // props든 data든 $변수든 밑에서 쓸땐 this써야함.
    methods : {
        send () {
            this.$emit('openModal',this.원룸들.title)
        }
    }

}
</script>

<style>

</style>