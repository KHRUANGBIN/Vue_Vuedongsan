<template>

  <Transition name="fade">
    <Modal @closemodal="modal = false"
    :oneroom="oneroom" :modal="modal"
    :click="click"/>
  </Transition>

  <div class="menu">
    <a v-for="i in menus" :key="i">{{i}}</a>
  </div>

  <Discount :dc = "dc" />

  <button @click="priceSort" >가격 순 정렬</button>
  <button @click="reverseSort" >가격 역순 정렬</button>
  <button @click="englishSort" >알파벳 순 정렬</button>
  <button @click="sortBack" >초기화</button>

  <Card @openmodal="modal = true; click = $event" :oneroom="oneroom[i]" v-for="(a,i) in oneroom" :key="i"/>

</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from  './Card.vue';

export default {
  name: 'App',
  data() {
    return {
      dc : 30,
      click : 0,
      oneroomOrigin : [...data],
      oneroom : data,
      modal : false,
      report : [0,0,0],
      menus : ['Home', 'Shop', 'About'],
      price : ['50', '60', '70'],
      products : ['역삼동원룸', '천호동원룸','마포구원룸'],
    }
  },
  methods: {
    priceSort(){
      this.oneroom.sort(function(a,b){
        return a.price-b.price
      })
    },
    sortBack(){
      this.oneroom = [...this.oneroomOrigin];
    },
    reverseSort(){
      this.oneroom.sort(function(a,b){
        return b.price-a.price
      })
    },
    englishSort(){
      this.oneroom.sort(function(a,b){
        return a.title.localeCompare(b.title);
      })
    },
  },

    mounted(){
      setInterval(() => {
        this.dc--;
      }, 1000);
  },

  components: {
    Discount,
    Modal,
    Card,
  }
}

</script>

<style>
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}



body {
  margin : 0;
}
div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
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
