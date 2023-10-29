<template>
  <div class="mainapp">
    <NavBar />
    <SearchFresh
      @search-input="handlerSearch"
      @max-price-input="handlerMaxPrice"
    />
    <div class="Fondo">
      <div class="filter">
        <p class="filter-title" v-if="showFilter">Buscar por:</p>
        <div class="filter-options" v-if="showFilter">
          <div class="flex">
            <input type="checkbox" v-model="filtroFruta" />
            <p>Frutas</p>
          </div>
          <div class="flex">
            <input type="checkbox" v-model="filtroVerdura" />
            <p>Verduras</p>
          </div>
          <div class="flex">
            <input type="checkbox" v-model="filtroDisponibilidad" />
            <p>Disponibles en el dia</p>
          </div>
          <div class="flex">
            <input type="checkbox" v-model="filtroEsOrganico" />
            <p>Organicos</p>
          </div>
          <div class="flex">
            <input type="checkbox" />
            <p>Todos</p>
          </div>
        </div>
        <p class="FiltroAvanzado" @click="showFilterHandler">
          Filtros avanzados
        </p>
      </div>

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

const filtroFruta = ref(false);
const filtroVerdura = ref(false);
const filtroDisponibilidad = ref(false);
const filtroEsOrganico = ref(false);

const showFilter = ref(false);

const searchInput = ref("");
const maxPrice = ref(null);

const showFilterHandler = () => {
  showFilter.value = !showFilter.value;
};

const handlerSearch = (input) => {
  searchInput.value = input;
};

const handlerMaxPrice = (price) => {
  maxPrice.value = +price;
};

const data = [
  {
    imagenPrincipal:
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQALlSFsF2y3k87L1QPizb8SISDIfN4jlgjrA&usqp=CAU",
    ratingStar: 5,
    nombreProducto: "Cebolla",
    precioProducto: 6500,
    tienda: "Despensa Catriel",
    disponibilidadDia: true,
    esFruta: false,
    esVerdura: true,
    esOrganico: true,
  },
  {
    imagenPrincipal:
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQM-nymmUBzAk7xVmKZ_c8H_2GLXXrrdbw-gA&usqp=CAU",
    ratingStar: 5,
    nombreProducto: "Tomate",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: true,
    esFruta: true,
    esVerdura: false,
    esOrganico: false,
  },
  {
    imagenPrincipal:
      "https://www.vidaorganica.com.co/wp-content/uploads/ajo-organico.jpg",
    ratingStar: 5,
    nombreProducto: "Ajo",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: false,
    esFruta: false,
    esVerdura: true,
    esOrganico: true,
  },
  {
    imagenPrincipal:
      "https://youdoit.fr/21964-large_default/semillas-de-zanahoria-organica-touchon.jpg",
    ratingStar: 5,
    nombreProducto: "Zanahoria",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: true,
    esFruta: false,
    esVerdura: true,
    esOrganico: false,
  },
  {
    imagenPrincipal:
      "https://www.cuerpomente.com/medio/2023/04/27/cuantas-calorias-tiene-una-manzana_2c000dbb_230427111605_900x900.jpg",
    ratingStar: 5,
    nombreProducto: "Manzana",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: false,
    esFruta: true,
    esVerdura: false,
    esOrganico: true,
  },
  {
    imagenPrincipal:
      "https://png.pngtree.com/thumb_back/fw800/background/20221112/pngtree-fresh-parsley-seasoning-organic-garnish-photo-image_28617432.jpg",
    ratingStar: 5,
    nombreProducto: "Perejil",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: true,
    esFruta: false,
    esVerdura: true,
    esOrganico: true,
  },
  {
    imagenPrincipal:
      "https://img.freepik.com/fotos-premium/sandia-organica-trozo-corte-longitudinalmente-sobre-fondo-blanco-aislado-trazado-recorte_54178-1998.jpg?w=2000",
    ratingStar: 5,
    nombreProducto: "Sandia",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: false,
    esFruta: true,
    esVerdura: false,
    esOrganico: false,
  },
  {
    imagenPrincipal:
      "https://i0.wp.com/shakeadito.com/wp-content/uploads/2022/08/Pinot-nuar_PORTADA-NOTA.jpg?fit=1370%2C929&ssl=1",
    ratingStar: 5,
    nombreProducto: "Uva",
    precioProducto: 9500,
    tienda: "Xinthy-Chop",
    disponibilidadDia: false,
    esFruta: true,
    esVerdura: false,
    esOrganico: false,
  },
];

const filteredData = computed(() => {
  const query = searchInput.value.toLowerCase().trim();
  const maxPriceValue = maxPrice.value;

  return data.filter((product) => {
    const nombreProductoMatches = product.nombreProducto
      .toLowerCase()
      .includes(query);
    const precioProductoPasses =
      maxPriceValue === null || product.precioProducto <= maxPriceValue;

    // Filtrar por tipo (Fruta o Verdura)
    const filtroFrutaPasses = !filtroFruta.value || product.esFruta;
    const filtroVerduraPasses = !filtroVerdura.value || product.esVerdura;

    // Filtrar por disponibilidad en el día
    const filtroDisponibilidadPasses =
      !filtroDisponibilidad.value || product.disponibilidadDia;

    // Filtrar por orgánico
    const filtroEsOrganicoPasses =
      !filtroEsOrganico.value || product.esOrganico;

    return (
      nombreProductoMatches &&
      precioProductoPasses &&
      filtroFrutaPasses &&
      filtroVerduraPasses &&
      filtroDisponibilidadPasses &&
      filtroEsOrganicoPasses
    );
  });
});
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
  font-family: "Plus Jakarta Sans", sans-serif;
}

.flex {
  display: flex;
}

.Fondo {
  display: flex;
  background-color: #f5f5f5;
  min-height: 100px;
  padding: 40px 100px;
}

input {
  margin-right: 5px;
}

.mainapp {
  overflow: hidden;
}

.filter-options {
  margin-top: 10px;
}

.row {
  display: flex;
  justify-content: center;
  gap: 50px;
  flex-wrap: wrap;
  width: 100%;
}

.filter {
  width: 200px;
  padding-inline: 8px;
}

.FiltroAvanzado {
  padding-top: 10px;
}
@import url("https://fonts.googleapis.com/css2?family=Anton&family=Plus+Jakarta+Sans:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,200&display=swap");
</style>
