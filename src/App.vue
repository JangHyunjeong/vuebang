<template>
  <div>
    <h2>12. 상품정렬기능과 데이터 원본 보존</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <DiscountBanner/>

  <button @click="sortPriceLowToHigh">가격낮은순정렬</button>
  <button @click="sortPriceHighToLow">가격높은순정렬</button>
  <button @click="sortTitle">상품명가나다순</button>
  <button @click="sortBack">되돌리기</button>
  
  <PopupModal @closeModal="closeModal" :productList="productList" :modalIdx="modalIdx" :modalIsOepn="modalIsOepn" :closeModal="closeModal"/>

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
      // array, object데이터의 각각 별개 사본을 만드려면
      // [...array자료]
      productListOriginal: [...productListData],
      productList: productListData,
      menuItem: ['Home', 'About', 'Products'],
      modalIdx: 0,
    };
  },

  methods: {
    increase(idx){
      this.productList[idx].reported++;
    },

    openModal(idx){
      this.modalIsOepn = true;
      this.modalIdx = idx;
    },

    closeModal(){
      this.modalIsOepn = false;
    },

    sortPriceLowToHigh(){
      // var array = [2,5,3];
      // sort() 는 사실 문자 정렬,ㄱㄴㄷ순.

      // 숫자 정렬은 다음과 같이
      // console.log(array.sort(function(a, b){
      //   return a - b;  // 음수면 a를 왼쪽으로 보내주세요
      // }))

      // 요즘은 sort 잘 안씀 - 원본 데이터가 변경되니까, map , filter 와 같은 메소드 쓰는게 나음
      // 아니면 sort를 쓰더라도 [...array] 사용하여 원본을 저장할 수 있음

      this.productList.sort(function(a,b){
        return a.price - b.price;
      });
    },

    sortPriceHighToLow(){
      this.productList.sort(function(a,b){
        return b.price - a.price;
      })
    },

    sortTitle(){
      this.productList.sort(function(a,b){
         let x = a.title;
         let y = b.title;

        if(x < y){
          return -1;
        }
        if(x > y) {
          return 1;
        }
        return 0;
      });
    },

    // 등호로 array를 집어넣으면 왼쪽 오른쪽 값을 공유해주세요~ 임
    // 그래서 [...array]자료 (카피본)을 집어넣어주세요
    sortBack(){
      this.productList = [...this.productListOriginal];
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
