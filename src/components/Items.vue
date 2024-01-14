<template>
  <div class="Items">
    <div class="card shadow p-3 mb-2" id="mainCard" v-for="item in searchResults" v-bind:key="item.id ">
      <div class="Picture">
        <img v-bind:src="baseImageUrl + item.appId + imageHeader" width="150">
      </div>
      <div class="RowOne">
        <div class="text text-white">Release Date
          <div class="infoText text-white">
            {{item.releaseDate}}
          </div>
        </div>
        <div class="text text-white">Publisher
          <div class="infoText text-white">
            {{item.publisher}}
          </div>
        </div>
        <div class="text text-white">Developer
          <div class="infoText text-white">
            {{item.developer}}
          </div>
        </div>
      </div>
      <div class="gameName text-white">
        {{item.name}}
      </div>
      <div class="RowTwo">
        <div class="text text-white">Platforms
          <div class="infoText text-white" v-for="item in item.platforms" v-bind:key="item.platforms">
            {{item}}
          </div>
        </div>
        <div class="text text-white">Tags
          <div class="infoText text-white" v-for="item in item.steamSpyTags" v-bind:key="item.steamSpyTags">
            {{item}}
          </div>
        </div>
      </div>
      <div class="RowThree">
        <div class="text text-white">Genres
          <div class="infoText text-white" v-for="item in item.genres" v-bind:key="item.genres">
            {{item}}
          </div>
        </div>
        <div class="text text-white">Categories
        <div class="infoText text-white" v-for="item in item.categories" v-bind:key="item.categories">
          {{item}}
        </div>
      </div>
      </div>
      <div id="buttonDiv">
      <b-button id="webButton" v-bind:href="webURL + item.appId" target="_blank">
        go to Steam
      </b-button>
      </div>
    </div>
  </div>
</template>
<script>

import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

export default {
  props: {
    name: String,
    releaseDate: String,
    publisher: String,
    platforms: String,
    categories: String,
    developer: String,
    genres: String,
    searchResults: [],
    URL: String
  },
  data() {
    return {
      baseImageUrl: 'https://steamcdn-a.akamaihd.net/steam/apps/',
      imageHeader: '/header.jpg',
      webURL: 'https://store.steampowered.com/app/'
    }
  }
}
</script>

<style scoped>
.Items{
  grid-column: 2;
}

.card{
  color: #1e1e1e;
  align-items: start;
  height: 200px;
  margin-bottom: 5px;
  margin-left: 10px;
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(5px, auto);
}

.card-container{
  margin-top: 20px;
  width: 70%;
}

.Picture {
  grid-column: 1;
  margin-top: 10px;
}

.RowOne {
  grid-column: 1;
  grid-row: 2;
}

.RowTwo{
  grid-column: 2;
  grid-row: 2;
}

.RowThree{
  grid-column: 3;
  grid-row: 2;
}

#webButton{
  grid-column: 3;
  color: white;
  background-color: #444140;
  font-size: 10px;
  width: 80px;
  height: 30px;
  justify-content: center;
}

#buttonDiv{
  grid-column: 1;
}

.text{
  padding: 5px;
  font-size: small;
  text-shadow: #0a0a0a;
}

.infoText{
  font-family: "Roboto Light";
  font-size: smaller;
  opacity: 0.7;
}

.gameName{
  font-family: "Roboto Medium";
  font-size: x-large;
  grid-column: 2;
  grid-column-end: 4;
}

</style>