<template>
  <div class="main">
    <h2>Del producto a tu mesa</h2>
    <h3>Buscar productos cerca</h3>
    <div class="custom-input">
      <input v-model="inputText" type="text" />
      <img :src="FondoImage" alt="" />
    </div>
    <div class="custom-input">
      <input v-model="maxNumber" type="text" />
    </div>
  </div>
</template>

<script setup>
import FondoImage from "./../assets/Group.png";
import { computed, defineEmits } from "vue";

const emits = defineEmits(["searchInput", "maxPriceInput"]);

const inputText = computed({
  get() {
    return "";
  },
  set(value) {
    emits("searchInput", value);
  },
});

const maxNumber = computed({
  get() {
    return "";
  },
  set(value) {
    emits("maxPriceInput", value);
  },
});
</script>

<style scoped>
.main {
  background-image: url(./../assets/fondo1.jpg);
  margin-top: -8px;
  padding-top: 80px;
  height: 85vh;
  background-position: center;
  background-size: cover;
  width: 100%;
  display: flex;
  color: white;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

h2 {
  font-size: 45px;
}

h3 {
  font-size: 20px;
  font-weight: 400;
}

.custom-input {
  display: flex;
  padding: 3px 10px;
  justify-content: space-between;
  margin-top: 10px;
  align-items: center;
  background-color: white;
  border-radius: 40px;
  width: 420px;
  z-index: 2;
  height: 35px;
  margin-bottom: 20px;
}

input {
  border: none; /* Eliminar el borde del input */
  z-index: 1;
  width: 100%;
  outline: none; /* Eliminar el borde de enfoque predeterminado */
}

.custom-input img {
  height: 25px;
}

input:focus {
  border: 0px;
}
</style>
