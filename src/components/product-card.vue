<template>
  <v-col sm="4" xs="12" md="3" id="card">
    <v-card max-width="400">
      <v-img height="200px" :src="imgUrl">
      </v-img>
      <v-card-title>${{ price }}</v-card-title>
      <v-card-subtitle class="pb-0">
        {{ condition }}
      </v-card-subtitle>

      <v-card-text class="text--primary">
        <h5>{{ name }}</h5>

        <div>{{ seller }}</div>
      </v-card-text>

      <v-card-actions>
        <v-btn color="cyan darken-4" text> Ver más </v-btn>
      </v-card-actions>
    </v-card>
  </v-col>
</template>
<script>
export default {
  props: ["imgUrl", "price", "condition", "name", "seller"],
};
</script>
<style>
  #card{
    padding: 15px 10px;
  }
</style>