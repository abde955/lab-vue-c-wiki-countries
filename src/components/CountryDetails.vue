<template>
    <div v-if="country" class="container">
      <h1>{{ country.name }}</h1>
      <img :src="flagUrl" alt="flag" class="img-fluid" />
      <p>Capital: {{ country.capital }}</p>
      <p>Area: {{ country.area }} km²</p>
      <p>Population: {{ country.population }}</p>
      <p>Region: {{ country.region }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  const country = ref(null);
  const flagUrl = `https://flagpedia.net/data/flags/icon/72x54/${route.params.alpha3Code.toLowerCase()}.png`;
  
  onMounted(async () => {
    try {
      const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${route.params.alpha3Code}`);
      if (response.ok) {
        country.value = await response.json();
      } else {
        console.error("Error fetching country details:", response.statusText);
      }
    } catch (error) {
      console.error("Error fetching country details:", error);
    }
  });
  </script>
  
  <style scoped>
  </style>
  
  
  