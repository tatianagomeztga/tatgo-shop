<template>
  <v-dialog v-model="details" max-width="800px">
    <v-card>
      <v-img class="black--text align-end" height="300px" :src="imgUrl">
      </v-img>
      <v-card-title>
        <span>{{ name }}</span>
      </v-card-title>
      <v-card-subtitle class="pb-0 white--text">
        {{ condition }}
      </v-card-subtitle>

      <v-card-text class="black--text">
        <p>{{ city }}</p>
        
        <h2>${{ price }}</h2>

        <p>Cantidad disponible: {{ availableQ }} <br>
          Cantidad vendida: {{ soldQ }} <br>
          Vendedor: {{ seller }}</p>
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