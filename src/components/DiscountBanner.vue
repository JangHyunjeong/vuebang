<template>
  <div class="discount">
    <h4>지금 가입하면 {{discountValue}}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'DiscountBanner',

  props:{
    discountValue: Number,
  }
}
</script>

<style>
.discount {
  background: gray;
  padding: 30px 20px;
  margin: 50px 0;
  color: white;
  font-size: 16px;
}
</style>

