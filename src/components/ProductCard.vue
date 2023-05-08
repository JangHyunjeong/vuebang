<template>
  <div class="product-item">
      <div class="product-item-img">
        <img :src=product.image>
      </div>
    <h4 @click="this.$parent.openModal(idx)" class="product-item-name">{{ product.title }}</h4>
      <p>{{ product.price }}</p>
      <button @click="this.$parent.increase(idx)">허위매물 신고</button>
      <span>신고 수 : {{product.reported}}</span>
  </div>
</template>

<script>
export default{
  name: "ProductCard",
  props:{
    product: Object,
    modalIdx: Number,
    modalIsOepn: Boolean
  }
}
</script>

<style>
.product-item {
  width: 500px;
  margin: 60px auto 0;
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