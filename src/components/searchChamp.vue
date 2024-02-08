<template>
    <div>
      <input v-model="searchChamp" @input="updateSearchChamp" type="text" placeholder="Search...">
      <p>{{ searchChamp }}</p>
    </div>
  </template>

<style>


</style>
  
  <script>
  export default {
    data() {
      return {
        searchChamp: ''
      };
    },
    methods: {
      updateSearchChamp(event) {
        this.searchChamp = event.target.value;
      }
    }
  };
  </script>