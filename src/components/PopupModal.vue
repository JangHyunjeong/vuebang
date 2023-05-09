
<template>
  <div class="modal-wrap" v-if="modalIsOepn">
    <div class="modal">
      <h4>{{ productList[modalIdx].title }}
        <button @click="$emit('closeModal')">닫기</button>
      </h4> 
      <div class="product-item-img">
        <img :src=productList[modalIdx].image>
      </div>
      <!-- 
      #1. input 안에 쓸만한 이벤트
      1. @input="" 
      : 인풋 안에다가 입력할 때 마다 js 실행해주세요

      2. @change=""
      : 입력하고 커서 다른데 찍으면 js 실행
    
      #2. $event
      function(e){} 에서 파라미터 e 와 같은 역할

      $event.target.value 현재 여기에서 나온 값
    
    
      #3. input에 입력한 내용 받아오기
      1. 
      <input @input="month = $event.target.value">
      
      2. 위의 코드의 축약버전 -->
      할부개월 : <input v-model.number="month" />
      

      <!-- 3. input 이외에도 v-model 사용가능
      <textarea v-model="month"></textarea>

      <select v-model="month">
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
      </select>

      <input type="checkbox" v-model="month" />
      - true, false로 값 반환 -->

      <p>{{ month }}개월 선택함 : {{ productList[modalIdx].price * month }}</p>
      <p>{{ productList[modalIdx].content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name : 'PopupModal',
  // 부모로부터 전달받은 데이터 등록
  // props : {데이터이름 : 자료형이름(Object, Array, Number, String...)}
  data(){
    return{
      month : 1,
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