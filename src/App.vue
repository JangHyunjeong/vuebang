<template>
  <div>
    <h2>2. v-for</h2>
    <div class="menu">
        <a v-for="(item, idx) in menuItem" :key="idx">{{ item }}</a>

        <!-- #2. v-for 기본 형태
        1) <a v-for="작명 in 몇회" :key="작명"></a> 
        - key를 꼭 써줘야함.

        2) <a v-for="작명 in 데이터어레이" :key="작명"></a> 

        2) <a v-for="(작명, 인덱스) in 데이터어레이" :key="인덱스"></a> 
      -->
    </div>
  </div>

  <div>
    <div v-for="(item, idx) in productList" :key="idx">
      <h4>{{ item.name }}</h4>
      <p>{{ item.price }}</p>
    </div>
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
          price: "10만원"
        },
        {
          name: "천호동원룸",
          price: "50만원"
        },
        {
          name: "마포구원룸",
          price: "100만원"
        }
    ],
      menuItem: ['Home', 'About', 'Products']
    };
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
</style>
