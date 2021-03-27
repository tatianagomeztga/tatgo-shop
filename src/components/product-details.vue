<template>
  <v-dialog v-model="details" max-width="800px">
    <v-card
      color="#393e46">
      <v-img class="black--text align-end" height="300px" :src="imgUrl">
        <v-card-title>
          <span>{{ name }}</span>
          <v-spacer></v-spacer>
        </v-card-title>
      </v-img>
      <v-card-subtitle class="pb-0 white--text">
        {{ condition }}
      </v-card-subtitle>

      <v-card-text class="white--text">
        <h5>{{ city }}</h5>
        
        <h2>${{ price }}</h2>

        <h4>Cantidad disponible: {{ availableQ }}</h4>
        <h4>Cantidad vendida: {{ soldQ }}</h4>
        <h4>Vendedor: {{ seller }}</h4>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="#00adb5" text @click="details = false"> Cerrar </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  props: [
    "details",
    "imgUrl",
    "name",
    "condition",
    "city",
    "price",
    "availableQ",
    "soldQ",
    "seller",
  ],
};
</script>