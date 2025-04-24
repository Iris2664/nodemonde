<script setup lang="ts">
  import { ref } from 'vue';
  import Card from "./components/Card.vue";

  const countries = ref();
  async function fetchCountries() {
    const response = await fetch("https://restcountries.com/v3.1/name/japan");
    const date = await response.json();
    countries.value = date;
  }
</script>

<template>
  <h1>Country Info</h1>
  <button @click="fetchCountries">Fetch</button>
  
  <Card
    v-for="country in countries"
    :key="country.name.common"
    :name="country.name.common"
    :image="country.flags.png"
    :tldList="country.tld"
  />
</template>

<style scoped>

</style>
