<template>
  <v-app id="app">
    <v-content>
      <t-header></t-header>
      <router-view/>
      <p-footer></p-footer>
    </v-content>
  </v-app>
</template>

<script>
import topHeader from "@/components/top-header.vue";
import footer from "@/components/footer.vue";

export default{
  components: {
    "t-header": topHeader,
    "p-footer": footer,
  }
}

</script>
<style>
  #app{
    background-image: url("assets/backgroundxl.png") !important;
    background-size: contain;
    background-repeat: no-repeat;

  }
</style>
