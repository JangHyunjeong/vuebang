<template>
  <div>
    <h2>3. click event</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>
    </div>
  </div>

  <div class="product-list">
    <div v-for="(item, idx) in productList" :key="idx" class="product-item">
      <div class="product-item-img">
        <!-- 이미지를 이렇게 넣으면 정상적으로 출력 안된다. require을 사용하자. -->
        <!-- <img src="]`./assets/room${idx}.jpg`"> -->
        <img :src="require(`./assets/room${idx}.jpg`)">
        
      </div>
      <h4>{{ item.name }}</h4>
      <p>{{ item.price }}</p>
      <button @click="increase(idx)">허위매물 신고</button>
      <span>신고 수 : {{item.reported}}</span>
    </div>

    <!-- #3. click event 기본형태
      1) v-on:click="자바스크립트 코드"
      2) @click="자바스크립트 코드"

      3) 함수는 이런식으로 @click="" 사이에 바로 넣어도 되고.. 
        method에서 함수를 따로 정의해도 된다.  
      <button @click="신고수++">허위매물 신고</button>

      기타) click 뿐 아니라, @mouseover="", @drag="" 등 다양한 이벤트 사용 가능
    -->
    
  </div>
</template>



<script>
export default {
  name: "App",
  // 필요한 데이터는 data() 바구니에 넣어줘야함.
  data() {
    return {
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
    }
  },
  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
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
</style>
