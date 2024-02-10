<template>
  <div className="search_input">
    <input v-model="summoner" type="text" placeholder="Ingrese el nombre del campeón" />
    <label for="">LAN</label>
    <button @click="searchSummoner">SEARCH</button>

  </div>
  <div className="summoner_card" v-if="playerName.name || playerData.summonerLevel">
    <img v-if="playerIcon.profileIconId" :src="'https://ddragon.leagueoflegends.com/cdn/14.3.1/img/profileicon/' + playerIcon.profileIconId + '.png'" alt="" />
    <p>
      <span className="titleName" v-if="playerName.name">{{ playerName.name }}</span>
      <span v-else>&nbsp;</span>
    </p>
    
    <p>
      <span className="titleLevel" v-if="playerData.summonerLevel">Summoner Level: {{ playerData.summonerLevel }}</span>
      <span v-else>&nbsp;</span>
    </p>
 
  </div>

</template>

<script>
import { ref, reactive } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const summoner = ref('');
    //add  a new property to the reactive object called "playerName" with an initial value of an empty
    const playerData = reactive({ summonerLevel: null });
    const playerName = reactive({name: null});
    const playerIcon = reactive({profileIconId:null});

    //api riot games
    const API_KEY = 'RGAPI-68d0a77d-e7a3-4d35-8efa-d5d951505279';


    //function  that makes a request to the api and get data about the summoner
    function searchSummoner() {
      const APICallString = `https://la1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${summoner.value}?api_key=${API_KEY}`;


      //using axios for  make http requests
      axios.get(APICallString)
        .then(response => {

          //save  in the variable playerData all the data returned by the response
          playerData.summonerLevel = response.data.summonerLevel;
          playerName.name = response.data.name;
          playerIcon.profileIconId = response.data.profileIconId;

        })

        //show ing error if the server doesn't respond or if there is any other kind of error
        .catch(error => {
          console.log("There was an error!");
        });
    }
    // return a object  with the functions and variables that we want to use in our template
    return { summoner, playerData, playerName, playerIcon, searchSummoner };
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

</style>