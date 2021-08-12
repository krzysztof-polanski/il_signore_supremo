<template>
  <div>
    <h1>Overlord Game</h1>
    <form action=""></form>
    <button class="do-not-click" @click.ctrl="getApiKey">USE WITH CAUSION (CTRL+Click): Get API Key</button>
    <button @click="createFullGame">Authenticate</button>
    <button @click="createNewGame">Create New Game</button>
    <button @click="getGameDetails">Get Game Details</button>
    <button @click="postNewGamerApi">Post New Gamer</button>
    <ul>
      <!-- <li v-for="(pair, index) in gameParameters.market" :key="index"> -->
        <MarketPair v-for="(pair, index) in gameParameters.market" :key="index" :pair="pair" />
        <!-- {{ pair.terrainTile }} -->
      <!-- </li> -->
    </ul>
    <ul>
      <li class="playerBoard" v-for="(playerBoard, index) in gameParameters.playerBoards" :key="index">
        <GameBoard :playerBoard="playerBoard" :index="index" v-show="this.player === index + 1" />
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import MarketPair from './MarketPair.vue';
import GameBoard from './GameBoard.vue';

export default {
  name: 'OverlordGame',
  props: {
    msg: String,
  },
  components: {
    MarketPair,
    GameBoard,
  },
  data() {
    return {
      userData: {
        user: 'polanski.krzysztof92@gmail.com',
        api_key: 'df5d0bf1-d615-4fd0-b023-2f9060b341aa',
      },
      token: '',
      paramsForGameCration: {
        game: 'Overboss',
        playerCount: 2,
      },
      url: 'http://board-games.pkp.corpnet.pl',
      play_uuid: '',
      gameParameters: {},
      player: 1,
    };
  },
  mounted() {
    this.createFullGame();
    // this.getGameDetails();
  },
  methods: {
    createNewGame() {
      console.log('New Game Created');
      axios.post(`${this.url}/api/plays/`, this.paramsForGameCration, {headers: {Authorization: `Bearer ${this.token}`}})
      .then((result) => {
        this.play_uuid = result.data.play_uuid;
        console.log(this.play_uuid)
      })
      .then(() => this.getGameDetails())
      .catch(console.error);
    },
    createFullGame() {
      console.log('Authentication Successful');
      axios.post(`${this.url}/authentication_token`, this.userData, {headers: {'Content-Type': 'application/json'}})
      .then((result) => {
        this.token = result.data.token;
        this.createNewGame();
      })
      .catch(console.error);
    },
    postNewGamerApi() {
      axios.post(`${this.url}/new-gamer`, {email: this.userData.user}, {headers: {'Content-Type': 'application/json'}})
      .then((result) => console.log(result))
      .catch((error) => console.log(`my error: ${error}`));
    },
    getApiKey() {
      axios.get(`${this.url}/reset-api-key/${this.userData.user}`)
      .then((result) => {
        this.userData.api_key = result.data.api_key;
        console.log(result.data.api_key);
      })
      .catch((error) => console.log(`my error: ${error}`));
    },
    getGameDetails() {
      console.log('Game details received');
      axios.get(`${this.url}/api/plays/${this.play_uuid}`, {headers: {Authorization: `Bearer ${this.token}`}})
      .then((result) => {
        // const gameDetails = result.data;
        console.log(result.data);
        this.gameParameters = result.data;
        console.log(this.gameParameters);
      })
      .catch((error) => console.log(`my error: ${error}`));
    },
  },
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style>
:root {
  --green: #42b983;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: var(--green);
}
button {
  background-color: var(--green);
  color: aliceblue;
  width: 12vw;
  aspect-ratio: 1 / 1;
  margin: 15px;
  padding: 10px;
  border: var(--green);
  border-radius: 50%;
  cursor: pointer;
  vertical-align: middle;
}
button:hover {
  
  box-shadow: 0 0 30px var(--green);
}
.do-not-click {
  background-color: #ff4455;
  opacity: 0.5;
  cursor: not-allowed;
}
.playerBoard {
  width: 80%;
}
</style>
