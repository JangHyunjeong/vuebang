<template>
  <div>
    <h2>6. components</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <!-- 
  #1. 컴포넌트 문법 왜씀?
  1. 구조 예뻐보일라고 
  2. 재사용성이 좋음. (반복적으로 등장하는 비슷한 UI 어디서든 간단하게 사용가능)
  
  -->

  <DiscountBanner/>

  <div class="modal-wrap" v-if="modalIsOepn">
    <div class="modal">
      <h4>{{ productList[modalIdx].title }}
        <button @click="closeModal">닫기</button>
      </h4> 
      <div class="product-item-img">
        <img :src=productList[modalIdx].image>
      </div>
      <p>{{ productList[modalIdx].price }}</p>
      <p>{{ productList[modalIdx].content }}</p>
    </div>
  </div>

  <div class="product-list">
    <div v-for="(item, idx) in productList" :key="item.id" class="product-item">
      <div class="product-item-img">
        <img :src=item.image>
      </div>
     <h4 @click="openModal(idx)" class="product-item-name">{{ item.title }}</h4>
      <p>{{ item.price }}</p>
      <button @click="increase(idx)">허위매물 신고</button>
      <span>신고 수 : {{item.reported}}</span>
    </div>
  </div>

</template>



<script>
// component 파일 가져다 쓴느법
// 1. vue 파일 import
// 2. 등록하고 (components 에)
// 3. 쓰기

import productListData from './data.js';
import DiscountBanner from './components/DiscountBanner';  // 왼쪽은 자유작명

export default {
  name: "App",

  data() {
    return {
      modalIsOepn: false,
      productList: productListData,
      menuItem: ['Home', 'About', 'Products'],
      modalIdx: 0,
    };
  },

  methods: {
    increase(idx){
      this.productList[idx].reported++;
    },

    openModal(idx) {
      this.modalIsOepn = true;
      this.modalIdx = idx;
    },

    closeModal(){
      this.modalIsOepn = false;
    }
  },

  components:{ 
    DiscountBanner: DiscountBanner  // 왼쪽은 자유작명
    // DiscountBanner 양 항이 같으면 하나만 써도 됨
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
button {
  cursor: pointer;
}
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
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

.product-list {
  width: 500px;
  margin: 0 auto;
}
.product-item {
  margin: 60px;
}
.product-item-img {
  width: 100%;
  height: 0;
  padding-bottom: 60%;
  position: relative;
  margin-bottom: 10px;
}
.product-item-img img {
  display: block;
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  object-fit: cover;
}
.product-item-name {
  cursor: pointer;
  margin-bottom: 5px;
}
.product-item p {
   margin-bottom: 5px
}

</style>
