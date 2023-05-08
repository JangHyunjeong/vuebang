
<template>
  <div class="modal-wrap" v-if="modalIsOepn">
    <div class="modal">
      <h4>{{ productList[modalIdx].title }}
        <button @click="$emit('closeModal')">닫기</button>
      </h4> 
      <div class="product-item-img">
        <img :src=productList[modalIdx].image>
      </div>
      <p>{{ productList[modalIdx].price }}</p>
      <p>{{ productList[modalIdx].content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name : 'PopupModal',
  // 부모로부터 전달받은 데이터 등록
  // props : {데이터이름 : 자료형이름(Object, Array, Number, String...)}
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