<script setup lang="ts">
  import { ref } from 'vue';
  import Card from "./components/Card.vue";

  const input = ref("");
  const countries = ref();

  async function fetchCountries() {
    const response = await fetch(`https://restcountries.com/v3.1/name/${input.value}`);
    const date = await response.json();
    countries.value = date;
  }
</script>

<template>
  <h1>Country Info</h1>

  <form @submit.prevent="fetchCountries">
    <input v-model="input" placeholder="coutrty name" />
    <button @click="fetchCountries">Fetch</button>  
  </form>
  
  
  <Card
    v-for="country in countries"
    :key="country.name.common"
    :name="country.name.common"
    :image="country.flags.png"
    :tldList="country.tld"
  />
</template>

<style scoped>
  form {
    padding: 2em;
    display: flex;
  }

  input {
    width: 200px;
    height: 1.5em;
    padding: 1em;
    border-radius: 1rem;
    border: 1px solid #d8d8d8;
    margin-right: 1em;
  }

  input:hover {
    border: 2px solid #334;
  }

  form button {
    margin-left: 1em;
    padding: 1em;
  }
</style>
