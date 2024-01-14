<template>
  <div class="Items">
      <div class="card shadow p-3 mb-2" v-for="item in list" v-bind:key="item.id ">
          <div class="RowOne">
            <img src="
https://steamcdn-a.akamaihd.net/steam/apps/10/header.jpg?t=1528733245" width="150">
          </div>
        <div class="gameName text-white">
            {{item.name}}
        </div>
        <div class="RowTwo">
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
          <div class="text text-white">Platforms
            <div class="infoText text-white" v-for="item in item.platforms" v-bind:key="item.platforms">
              {{item}}
            </div>
          </div>
        </div>
        <div class="RowThree">
          <div class="text text-white">Categories
            <div class="infoText text-white" v-for="item in item.categories" v-bind:key="item.categories">
              {{item}}
            </div>
          </div>
          <div class="text text-white">Genres
            <div class="infoText text-white" v-for="item in item.genres" v-bind:key="item.genres">
              {{item}}
            </div>
          </div>
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
  name: "items",
  data(){
    return {list:undefined}
  },

  mounted() {
    Vue.axios.get('http://localhost:8080/api/search?search=').then((res) =>{
      this.list=res.data.searchResults;
    })
  }
}
</script>

<style scoped>

.card{
  color: #1e1e1e;
  background-color: #444140;
  align-items: start;
  width: 550px;
  height: auto;
  margin-bottom: 5px;
  margin-left: 10px;
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(3, 175px);
  grid-auto-rows: minmax(5px, auto);
}

.Items{
  margin-top: 20px;
}

.RowOne {
  grid-column-start: 1;
  grid-row: 1 / 3;
  margin-top: 50px;
}

.RowTwo{
  grid-column: 2;
}

.RowThree{
  grid-column: 3;
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