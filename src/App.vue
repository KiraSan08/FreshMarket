<template>
  <div class="mainapp">
    <NavBar />
    <SearchFresh
      @search-input="handlerSearch"
      @max-price-input="handlerMaxPrice"
    />
    <div class="Fondo">
      <div class="row">
        <ProductsFresh
          v-for="product in filteredData"
          :key="product.nombreProducto"
          :imagen-principal="product.imagenPrincipal"
          :rating-star="product.ratingStar"
          :nombre-producto="product.nombreProducto"
          :precio-producto="product.precioProducto"
          :tienda="product.tienda"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import NavBar from "./components/NavBar.vue";
import ProductsFresh from "./components/ProductsFresh.vue";
import SearchFresh from "./components/SearchFresh.vue";

const searchInput = ref("");
const maxPrice = ref(null);

const handlerSearch = (input) => {
  searchInput.value = input;
};

const handlerMaxPrice = (price) => {
  maxPrice.value = +price;
};

const data = [
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Cebolla",
    precioProducto: 6500,
    tienda: "Despensa Catriel",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Tomate",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Ajo",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Zanahoria",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Manzana",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Perejil",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Arroz",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
  {
    imagenPrincipal:
      "https://www.abc.com.py/resizer/HlhgdQ4VoENqBARol0hxMtEtlaM=/fit-in/770x495/smart/filters:format(webp)/arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/I7ZKCM6NJZDHJAR6UZMSB5KCWA.jpg",
    ratingStar: 5,
    nombreProducto: "Zapallo",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
  },
];

const filteredData = computed(() => {
  const query = searchInput.value.toLowerCase().trim();
  const maxPriceValue = maxPrice.value;

  if (query === "" && maxPriceValue === null) {
    return data;
  } else {
    return data.filter((product) => {
      const nombreProductoMatches = product.nombreProducto
        .toLowerCase()
        .includes(query);
      const precioProductoPasses =
        maxPriceValue === null || product.precioProducto <= maxPriceValue;
      return nombreProductoMatches && precioProductoPasses;
    });
  }
});
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
  font-family: "Plus Jakarta Sans", sans-serif;
}

.Fondo {
  background-color: #f5f5f5;
  min-height: 100px;
  padding: 40px 100px;
}

.mainapp {
  overflow: hidden;
}

.row {
  display: flex;
  justify-content: center;
  gap: 50px;
  flex-wrap: wrap;
  width: 100%;
}
@import url("https://fonts.googleapis.com/css2?family=Anton&family=Plus+Jakarta+Sans:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,200&display=swap");
</style>
