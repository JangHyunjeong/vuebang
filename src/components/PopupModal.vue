
<template>
  <!-- #방법1.
  <div class="modal-animation" :class="{ opened : modalIsOepn}"> -->

  <!-- #방법2.
  transition tag 사용가능
  1. 애니메이션을 주고싶은 요소를 하단 태그로 바꾸기
  <transition name="작명"></transition>
  2. css 넣기 - 시작
     .작명-enter-from { 시작 스타일 }
     .작명-enter-active { transition }
     .작명-enter-to { 끝날시 스타일} 

     .작명-leave-from { 시작 스타일 }
     .작명-leave-active { transition }
     .작명-leave-to { 끝날시 스타일} 
  -->

  <transition name="fade">
    <div class="modal-wrap" v-if="modalIsOepn">
      <div class="modal">
        <h4>{{ productList[modalIdx].title }}
          <button @click="$emit('closeModal')">닫기</button>
        </h4> 
        <div class="product-item-img">
          <img :src=productList[modalIdx].image>
        </div>

        할부개월 : 
        <!-- <input v-model.number="month" /> -->

        <!-- ** 한글의 경우, v-model과 watch사용시, 실시간 데이터 확인이 어렵다 (IME) 이러너 경우, @input 사용하여, 실시가나 데이터를 확인할 수 있다. -->
        <input @input="month = $event.target.value" :value=month />
        
        <!-- 
        <input v-model.number="month" type="range" min="1" max="12" /> -->

        <p>{{ month }}개월 선택함 : {{ productList[modalIdx].price * month }}</p>
        <p>{{ productList[modalIdx].content }}</p>
      </div>
    </div>
  <!-- </div> -->
</transition>
</template>

<script>
export default {
  name : 'PopupModal',
  data(){
    return{
      month : 1,
    }
  },
  /* 데이터 감시하려면 
  watch:{
    감시할데이터(){}
  }*/
  watch : {
    // month라는 데이터가 변할때마다 watcher도 실행됨
    month(value){  // month(value, b) 파라미터는 2개까지 입력 가능한다. value: 변경 후 데이터, b: 변경 전 데이터
      if(isNaN(value) == true || value == ' ') {
        alert('숫자만 입력해주세요');
        this.month = 1;
        value = 1;
      }
      if(value < 1 || value > 12) {
        alert('1~12 사이의 숫자를 입력해주세요')
      }
    }
  },
  props : {
    productList : Array,
    modalIdx: Number,
    modalIsOepn: Boolean,
  }
}
</script>

<style>

.modal-wrap {
  width: 100%;
  height: 100%;
  padding: 20px;
  background-color: rgba(0,0,0,0.5);
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
}

/* 방법1 */
.modal-animation{
  opacity: 0;
  transition: all 0.3s;
}
.modal-animation.opened {
  opacity: 1;
}

/* 방법2 */
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.3s;
}
.fage-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 0.3s;
}
.fade-leave-to {
  opacity: 0;
}

.modal {
  width: 100%;
  min-height: 200px;
  background-color: white;
  border-radius: 8px;
  padding: 20px;
}
.modal h4 {
  display: flex;
  justify-content: space-between;
  margin-bottom: 50px;
}
.modal button {
  display: block;
  width: 50px;
  height: 30px;
  background: black;
  color: #fff;
  font-size: 14px;
  border: 0;
  border-radius: 5px;
}
</style>