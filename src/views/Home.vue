<template>
  <div class="">

    <p-card></p-card>
    <ul>
      <li v-for="product in products" :key="product.id">{{ product.title }}</li>
    </ul>
  </div>
</template>

<script>
  import productCard from '@/components/product-card.vue';
  import axios  from "axios";
  export default{
    name: "Home",
    components: {
      "p-card": productCard,
    },
    data(){
      return{
        baseUrl: "https://api.mercadolibre.com/sites/MCO/search?q=",
        search: '',
        products: [],
        empyP: true,
        productSelect: {},
      }
    },
    mounted(){
      this.getProducts();
    },
    methods: {
      async getProducts(){
        if(this.search.length > 0){
          const url= `${this.baseUrl}${this.search}`;
          try{
            let datos = await axios.get(url)
            .then(respuesta => this.products = respuesta.data.results);
            if(datos.data.results.length > 0){
              this.products = await datos.data.results;
              this.empyP = false;
            }else{
              this.empyP = true;
            }
          }catch(error){
            console.log(error);
          }finally{
            console.log("finally");
          }

        }else{
          try{
            let datos = await axios.get(`https://api.mercadolibre.com/sites/MCO/search?q=Motorola%20G6`)
            .then(respuesta => this.products = respuesta.data.results);
            if(datos.data.results.length > 0){
              this.products = await datos.data.results;
              this.empyP = false;
            }else{
              this.empyP = true;
            }
          }catch(error) {
            console.log(error);
          }finally {
            console.log("Finally del else");
          }
        };
        console.log(this.products);
      },
    },
  };
</script> 
