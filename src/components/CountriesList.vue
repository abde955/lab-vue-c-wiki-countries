<template>
    <div class="container">
      <h1>Countries</h1>
      <ul class="list-group">
        <router-link
          v-for="country in countries"
          :key="country.alpha3Code"
          :to="{ name: 'country-details', params: { alpha3Code: country.alpha3Code } }"
          class="list-group-item list-group-item-action"
        >
          {{ country.name }}
        </router-link>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const countries = ref([]);
  
  onMounted(async () => {
    try {
      const response = await fetch('https://ih-countries-api.herokuapp.com/countries');
      countries.value = await response.json();
    } catch (error) {
      console.error("Error fetching countries:", error);
    }
  });
  </script>
  
  <style scoped>
  </style>
  
  
  
  