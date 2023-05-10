<template>
  <div>
    <h2>13. life cycle</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <DiscountBanner v-if="showDiscount" :discountValue="discountValue"/>

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

  data() {
    return {
      showDiscount: true,
      discountValue: 30,
      modalIsOepn: false,
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

    sortBack(){
      this.productList = [...this.productListOriginal];
    },
  },
  // life cycle 왜쓰는지? - life cycle hook 쓸라고
  // 종류 : beforeCreate() , created() , beforeMount() , mounted() , beforeUpdate() , updated() , beforeUnmount() , unmounted()  

  // updated() : 재랜더링
  
  // 서버한테 데이터 요청할때 
  // html생성 전, 데이터만 존재할때
  created(){
  },

  mounted() {
    var decreaseSale = setInterval(() => {
        this.discountValue = this.discountValue-1;

        if(this.discountValue <= 0) {
          clearInterval(decreaseSale);
        }
      }, 1000); 
  },

  // mount된 후
  // mounted(){
  //   setTimeout(() => {
  //     // 바깥에 있는 this를 가져오고싶으면 arrow function 사용
  //     this.showDiscount = false;
  //     console.log('hhh')
  //   }, 2000);
  // },


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
