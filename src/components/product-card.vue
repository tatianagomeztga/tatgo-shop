<template>
  <v-col sm="4" xs="12" md="2" id="card">
    <v-card max-width="400">
      <v-img height="200px" :src="imgUrl"> </v-img>
      <v-card-title>${{ price }}</v-card-title>
      <v-card-subtitle class="pb-0">
        {{ condition }}
      </v-card-subtitle>

      <v-card-text class="text--primary">
        <h5>{{ name }}</h5>

        <div>{{ city }}</div>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="#00adb5" text @click="details = true"> Ver más </v-btn>
      </v-card-actions>
    </v-card>
    <p-details
      v-if="details"
      :details="details"
      :imgUrl="imgUrl"
      :name="name"
      :condition="condition"
      :city="city"
      :price="price"
      :availableQ="available"
      :soldQ="sold"
      :seller="seller"
    >
    </p-details>
  </v-col>
</template>
<script>
import productDetails from "@/components/product-details.vue";
export default {
  props: [
    "imgUrl",
    "price",
    "condition",
    "name",
    "city",
    "seller",
    "available",
    "sold",
  ],
  components: {
    "p-details": productDetails,
  },
  data() {
    return {
      details: false,
    };
  },
};
</script>
<style>
#card {
  padding: 15px 10px;
}
</style>