<template>
  <div>
    <h2> 1. 데이터 바인딩</h2>
    <h4 :class="h4Class" :style="h4Style">{{ products[0] }}</h4>
    <p>{{ price1 }}만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price2 }} 만원</p>
  </div>

   <!-- 
  #1. 데이터 바인딩

  ** 데이터 바인딩 하는 이유
  1) html 에 하드코딩 해 놓으면 나중에 변경 어려움
  2) (중요) 뷰가 제공하는 실시간 자동 렌더링 기능을 쓸수 있음. (data 변경 시, 바인딩된 데이터도 자동으로 변경)
  - 자주 변할 것 같은 데이터는 이런식으로 변경
  - 자주 변경될일 없는애들은 굳이 안바꿔도 됌
  - html 속성도 데이터바인디 가능 - :style 이런식으로 표시해야함
  -->
</template>



<script>
export default {
  name: "App",
  // 필요한 데이터는 data() 바구니에 넣어줘야함.
  data() {
    return {
      price1: 80,
      price2: 100,
      h4Style: "color:blue",
      h4Class: "h4Class",
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
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

</style>
