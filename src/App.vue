<template>
  <div>
    <h2>7. props</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>


  <DiscountBanner/>
  
  <!-- 
  #1. Props
  * 자식 컴포넌트가 부모가 가진 데이터 쓰고싶으면 props문법으로 전송해야함. 
  * props 받아온거는 read-only임. 받아온거 자식에서 수정하면 큰일남

  * 전송하는법
    1. 데이터 보내고
    - 부모 vue파일에서 아래 형식으로 보내면됨
    * 형식
     <PopupModal :데이터이름="데이터이름" />
     <PopupModal v-bind:데이터이름="데이터이름" />

    2. 등록하고
    - 자식 vue 파일에서 props에 등록하면 됨

    3. 쓰셈
    - 그냥 쓰셈.
    
    * 번외
    부모의 함수를 쓰고싶다면.. 함수는 보내지 않고, this.$parent.함수명을 사용하셈
  -->

  <!--
  컴포넌트 만들때 잘 생각해서 만들어야해 - props를 어떻게 관리해야할지 골치아파짐 
  1. data만들때, 부모도 쓰는 데이터라면, 부모 컴포넌트에 만들어두셈
  -> data를 상위로 전송하는게 더 어렵기 때문 ㅜ
  -->

  <PopupModal :productList="productList" :modalIdx="modalIdx" :modalIsOepn="modalIsOepn" :closeModal="closeModal"/>

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
import productListData from './data.js';
import DiscountBanner from './components/DiscountBanner';  // 왼쪽은 자유작명
import PopupModal from './components/PopupModal';

export default {
  name: "App",

  // 데이터는 한곳에 보관함. 그리고 필요하면 가져다 씀 -> props 이용
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
    DiscountBanner: DiscountBanner,
    PopupModal
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
