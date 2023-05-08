<template>
  <div>
    <h2>4. v-if 모달창 만들기</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <!-- 
  #1. 동적인 UI 만드는법
  1. UI의 현재 상태를 데이터로 저장해둠
  2. 데이터에 따라 UI가 어떻게 보일지 작성
  
  
  #2. v-if
  1. 기본형태
  <div v-if="조건식">
  조건식이 참일때만, 해당 엘리먼트를 마크업
 
 
  2. v-if와 함께 사용할 수 있는것
  <div v-if="조건식">
    안녕하세요
  </div>

  <div v-else="조건식">
    안녕하세요
  </div>

  <div v-else>
    안녕하세요
  </div>

  -->

  <div class="modal-wrap" v-if="modalIsOepn">
    <div class="modal">
      <h4>상세 페이지
        <button @click="closeModal">닫기</button>
      </h4>  
      <p>상세페이지 설명 영역입니다.</p>
    </div>
  </div>

  <div class="product-list">
    <div v-for="(item, idx) in productList" :key="idx" class="product-item">
      <div class="product-item-img">
        <img :src="require(`./assets/room${idx}.jpg`)">
        
      </div>
      <h4 @click="openModal" class="product-item-name">{{ item.name }}</h4>
      <p>{{ item.price }}</p>
      <button @click="increase(idx)">허위매물 신고</button>
      <span>신고 수 : {{item.reported}}</span>
    </div>

    
  </div>
</template>



<script>
export default {
  name: "App",
  // 필요한 데이터는 data() 바구니에 넣어줘야함.
  // 이 데이터 저장 공간을 state라고한다.
  // ui의 상태를 저장하는 공간이기도 함.
  data() {
    return {
      modalIsOepn: false,
      productList: [
        {
          name : "역삼동원룸",
          price: "10만원",
          reported: 0,
        },
        {
          name: "천호동원룸",
          price: "50만원",
          reported: 0,
        },
        {
          name: "마포구원룸",
          price: "100만원",
          reported: 0,
        }
    ],
      menuItem: ['Home', 'About', 'Products'],
    };
  },

  // 필요한 함수는 method 바구니에 정의해준다.
  // data에 있는 자료를 사용하고 싶을때는 this.자료명 으로 정의 해줘야함! 
  methods: {
    increase(idx){
      this.productList[idx].reported++;
    },

    // 모달 열기 함수 추가
    openModal() {
      this.modalIsOepn = true;
    },

    closeModal(){
      this.modalIsOepn = false;
    }
  },
  components: {},
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
