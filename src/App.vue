<template>
  <div>
    <h2>8. custom event</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <DiscountBanner/>
    <PopupModal @closeModal="closeModal" :productList="productList" :modalIdx="modalIdx" :modalIsOepn="modalIsOepn" :closeModal="closeModal"/>

    <!-- emit으로 보낸 이벤트는 아래와같이 수정
      $event는 자식에서 보낸 데이터는 이렇게 받아올 수 있다. 
    @openModal="modalIsOepn = true; modalIdx = $event" -->
    <ProductCard @openModal="openModal($event)" @increase="increase($event)" :product="productList[idx]" :modalIdx="modalIdx" :modalIsOepn="modalIsOepn" v-for="(item, idx) in productList" :key="idx"/>

</template>



<script>
import productListData from './data.js';
import DiscountBanner from './components/DiscountBanner';
import PopupModal from './components/PopupModal';
import ProductCard from './components/ProductCard';

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
    PopupModal,
    ProductCard
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
</style>
