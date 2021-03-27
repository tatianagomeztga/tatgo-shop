<template>
  <v-container>
    <v-container class="text-center">
      <form>
        <v-text-field
          outlined
          label="Presiona enter para buscar"
          append-icon="mdi-magnify"
          v-model="search"
          @keypress="enterSearch($event)"
        ></v-text-field>
      </form>
    </v-container>
    <v-row no-gutters v-if="isSearchSuccess">
      <p-card
        v-for="product in products"
        :key="product.id"
        :imgUrl="product.thumbnail"
        :price="product.price"
        :condition="product.condition"
        :name="product.title"
        :city="product.seller_address.city.name"
        :seller="product.seller.id"
        :available="product.available_quantity"
        :sold="product.sold_quantity"
      >
      </p-card>
    </v-row>
    <div class="text-center" v-if="!isSearchSuccess" style="margin: 30px">
      <h2>{{ message }}</h2>
    </div>
    <div class="text-center">
      <v-pagination
        v-if="isSearchSuccess"
        v-model="currentPage"
        :length="totalProducts"
        :per-page="limit"
        @input="changePage"
        circle
        color="#00adb5"
      ></v-pagination>
    </div>
  </v-container>
</template>

<script>
import productCard from "@/components/product-card.vue";
import axios from "axios";
export default {
  name: "Home",
  components: {
    "p-card": productCard,
  },
  data() {
    return {
      baseUrl: "https://api.mercadolibre.com/sites/MCO/search",
      search: "",
      offset: 0,
      limit: 50,
      primaryResults: 1000,
      isSearchSuccess: false,
      totalProducts: 0,
      products: [],
      seller: [],
      currentPage: 1,
      message: "Buscando...",
    };
  },
  mounted() {
    this.getProductsDefault();
  },
  methods: {
    async getProducts(search, offset, limit) {
      if (this.search) {
        this.message = "Buscando";
        try {
          let datos = await axios.get(this.baseUrl, {
            params: {
              q: search,
              offset: offset,
              limit: limit,
            },
          });
          if (datos.data.results.length > 0) {
            this.products = await datos.data.results;
            let total = await datos.data.paging.total;
            this.totalProducts = Math.ceil(total / this.limit);
            this.isSearchSuccess = true;
          } else {
            this.isSearchSuccess = false;
            this.message = "No se encontraron resultados";
          }
        } catch (error) {
          console.log(error);
        }
      }
    },
    async changePage(page) {
      this.isSearchSuccess = false;
      this.offset = this.limit * (page - 1);
      try {
        this.getProducts(this.search, this.offset, this.limit);
      } catch (error) {
        console.log(error);
      }
    },
    async getProductsDefault() {
      try {
        let datos = await axios.get(
          `https://api.mercadolibre.com/sites/MCO/search?q=Motorola%20G6`
        );
        //.then((respuesta) => (this.products = respuesta.data.results));
        if (datos.data.results.length > 0) {
          this.search="Motorola G6"
          let total = await datos.data.paging.total;
          this.totalProducts = Math.ceil(total / this.limit);
          this.products = await datos.data.results;
          this.isSearchSuccess = true;
        } else {
          this.isSearchSuccess = false;
          this.message = "No se encontraron resultados";
        }
      } catch (error) {
        console.log(error);
      }
    },
    enterSearch(event) {
      if (event.keyCode === 13) {
        this.getProducts(this.search, this.offset, this.limit);
      }
    },
    async sellerName(id) {
      let user = await axios.get(`https://api.mercadolibre.com/users/${id}`);
      let nick = await user.data.nickname;
      console.log(nick);
      this.seller(nick);
    },
  },
};
</script> 
