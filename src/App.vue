<template>


<div class="menu">
    <a v-for="names in menus" :key="names">{{ names }}</a>
    <!-- 메뉴 안에 있는 이름을 가져온다. -->
</div>

<Discount v-if="showDiscount == true" :discountNum ="discountNum" />

<button @click="priceSort">가격낮은순 정렬</button><br/>
<button @click="priceHighSort">가격높은순 정렬</button><br/>
<button @click="ganadaSort">가나다순 정렬</button><br/>
<button @click="sortBack">되돌리기</button>

<transition name="fade">

  <Modal @closeModal="modal_status =$event" :onerooms="onerooms" :press="press" :modal_status="modal_status"/>

</transition>

<Card @openModal="modal_status= true; press = $event" :items = "onerooms[i]" v-for="(val,i) in onerooms" :key="val"/>

</template>
<!-- 
  <ul>
    <div v-for="(item,index) in products" :key="index">
    <h4 class="font-bold">{{ item }} </h4>
    <p> {{ moneys[index] }} </p>
    </div>
  </ul> -->

<script>
import data from './assets/products.js';
import Discount from './components/Discount.vue';
import Modal from './components/Modal.vue';
import Card from './components/Card.vue';

export default {
  name: 'App',
  data(){
    return {
      discountNum: 40,
      showDiscount: true,
      originData: [...data],
      오브젝트 : {name:'kim', age:20},
      press: 0,
      onerooms: [...data],
      modal_status : false, 
      count: [0,0,0],
      moneys:['80','70','60'],
      menus:['home','products','about'],
      products:['역삼동 원룸','천호동 원룸','마포동원룸'],
    }
  },
  methods : {
      increase1(idx){
        // 큰 오브젝트 안에 있는거 사용할때 this쓰기 
        this.count[idx] +=1;
      },
      sortBack(){
        this.onerooms =  [...this.originData];
        
      },
      priceHighSort(){
        this.onerooms.sort(function(a,b){
          return  b.price- a.price;
        });
      },
      ganadaSort(){
         this.onerooms.sort(function(a,b){
          var aa = a.title.toUpperCase();
          var bb = b.title.toUpperCase();

          return aa < bb ? -1 :aa > bb ? 1 : 0;
         });
      },
      priceSort(){
        // sort 문자순 정렬
        var array = this.onerooms;
        array.sort(function(a,b){
          return a.price - b.price;
        });
      },
     
  },
  mounted() {
      
    setInterval(()=>{
      if(this.discountNum > 0){
       this.discountNum-=1;
      }else{
        this.discountNum = 40;
      }
    }, 1000);

  },
  components: {
    Discount : Discount, //Discount,얘도 가능
    Modal: Modal,
    Card: Card
  }
}
</script>

<style>
.fade-enter-from { transform: translateY(-1000px);}
.fade-enter-active {transition: all 1s;}
.fade-enter-to {transform: translateY(0px);}


.fade-leave-from {opacity: 1;}
.fade-leave-active{ transition: all 1s}
.fade-leave-to {opacity:0;}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
.font-bold{
            font-weight: bold;
}
.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
color: white;
padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}


</style>
