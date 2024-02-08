<template>
  <div>
    <input v-model="champ" type="text" placeholder="Ingrese el nombre del campeón" />
    <button @click="searchSummoner">Buscar</button>
    <p>
      <span v-if="playerName.name">Nombre del jugador: {{ playerName.name }}</span>
      <span v-else>&nbsp;</span>
    </p>
    <p>
      <span v-if="playerData.summonerLevel">Nivel del invocador: {{ playerData.summonerLevel }}</span>
      <span v-else>&nbsp;</span>
    </p>
    <img :src="'https://ddragon.leagueoflegends.com/cdn/14.3.1/img/profileicon/' + playerData.profileIconId + '.png'" alt="" />
  </div>
</template>

<script>
import { ref, reactive } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const champ = ref('');
    const playerData = reactive({ summonerLevel: null });
    const playerName = reactive({ name: null });
    const playerIcon = ref('');

    const API_KEY = 'RGAPI-106c2436-5dff-425f-bcb3-e1bebefbef64';

    function searchSummoner() {
      const APICallString = `https://la1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${champ.value}?api_key=${API_KEY}`;

      axios.get(APICallString)
        .then(response => {
          playerData.summonerLevel = response.data.summonerLevel;
          playerName.name = response.data.name;
          playerIcon.profileIconId = response.data.profileIconId;
        })
        .catch(error => {
          console.log("There was an error!");
        });
    }

    return { champ, playerData, playerName, playerIcon, searchSummoner };
  },
};
</script>