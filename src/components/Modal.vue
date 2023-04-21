<!-- 카멜 case로 쓰기 -->
<template >
   
<div class="black-bg" v-if="modal_status == true">
    <div class="white-bg">
      <img :src="onerooms[press].image"  alt="no_image" style="width:100%">
        <h4>{{onerooms[press].title}}</h4>
        <p>{{ onerooms[press].content }}</p>
        <input v-model.number="month"/>
        <p>{{ month }}개월 선택 : {{ onerooms[press].price * month }}원</p>
        <button @click="close">닫기</button>
    </div>
</div>
</template>
<script>


export default {
    name:'Modal' ,
    data(){
      return{
        month: 1,
      }
    },
    watch : {
        month(val){
        if(val > 12){
            alert('13이상 입력하지 마셈');
        }
        if(isNaN(val)== true){
            alert('숫자만 입력해주세요');
            this.month= 1;
        }
     }
    },
    props : {
        onerooms: Array,
        modal_status: Boolean,
        press: Number
    },
   methods : {
    close(){
        this.$emit('closeModal',false);
    }
   },
   updated() {
    if(this.month == 2){
        alert('2를 입력하셨습니다.');
    }
   },
    
    
}
</script>
<style>
body {
    margin: 0;
}
div {
    box-sizing: border-box;
}
.black-bg {
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.5);
    position: fixed;
    padding: 20px;
}
.white-bg {
    width: 100%;
    background-color: white;
    border-radius: 8px;
    padding: 20px;
}

</style>