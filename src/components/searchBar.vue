<template>
    <div>
      <input v-model="champ" type="text" placeholder="Ingrese el nombre del campeón" />
      <button @click="searchSummoner">Search</button>
      <p>Summoner Level : {{ playerData.summonerLevel }}</p>
    </div>
  </template>
  
  <script>
  import { ref, reactive } from 'vue';
  import axios from 'axios';
  
  export default {
    setup() {
      const champ = ref('');
      const playerData = reactive({ summonerLevel: null });
      const API_KEY = 'RGAPI-106c2436-5dff-425f-bcb3-e1bebefbef64';
  
      function searchSummoner() {
        const APICallString = `https://la1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${champ.value}?api_key=${API_KEY}`;
  
        axios.get(APICallString)
          .then(response => {
            playerData.summonerLevel = response.data.summonerLevel;
          })
          .catch(error => {
            console.log("There was an error!");
          });
      }
  
      return { champ, playerData, searchSummoner };
    },
  };
  </script>

<style>
    p{
        color:white
    }
    input::placeholder{
        text-align: center;
    }
    button{
        margin-top:1rem;
    }

</style>