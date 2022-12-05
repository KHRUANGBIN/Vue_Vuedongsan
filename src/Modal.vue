<template>
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <img :src="oneroom[click].image" style="width:100%">
      <h4>{{oneroom[click].title}}</h4>
      <p>{{oneroom[click].content}}</p> 
      <!-- <input @input="month = $event.target.value">      -->
      <input v-model.number="month">
      <p> {{ month }}개월 선택함 : {{oneroom[click].price * month}}원</p>
      <button @click="$emit('closemodal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Modal',
    data(){
      return {
        month : "",
      }
    },
    watch : {
      month(a){
        if(isNaN(a) == true){
          alert('숫자만 적어라')
          this.month = "";
        }
      }
    },
    beforeUpdate(){
        if (this.month == 2){
          alert('싫어')
      }
    },
    props: {
        oneroom : Array,
        click : Number,
        modal : Boolean,
    }
}
</script>

<style>

</style>