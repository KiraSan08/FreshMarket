<template>
  <div class="product">
    <img :src="props.imagenPrincipal" alt="" />
    <div class="reviews">
      <img :src="star" alt="" />
      <img :src="star" alt="" />
      <img :src="star" alt="" />
      <img :src="star" alt="" />
      <img :src="star" alt="" />
    </div>
    <p class="title">{{ nombreProducto }}</p>
    <p class="secundary">por kilo</p>
    <p class="precio">{{ precioProducto }}</p>
    <p class="secundary">
      Tienda: <a href="#">{{ tienda }}</a>
    </p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import star from "./../assets/start.png";
const props = defineProps({
  imagenPrincipal: String,
  ratingStar: Number,
  nombreProducto: String,
  precioProducto: Number,
  tienda: String,
});
</script>

<style scoped>
.products {
  background-color: #f5f5f5;
}

.productRow {
  display: flex;
  margin-top: 30px;
  height: 350px;
  width: 100%;
  justify-content: center;
  gap: 30px;
}

.product {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: white;
  padding: 20px;
  height: 270px;
  border-radius: 8px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1);
  width: 200px;
}

.product img {
  height: 160px;
  border-radius: 8px;
}

.reviews img {
  height: 15px;
}

.title {
  font-weight: 600;
}

.precio {
  font-size: 19px;
}
</style>
