<template>
  <div id="app">
    <div class="head w-50 mx-auto justify-content-center">
      <img class="logo" alt="Vue logo" width=700 src="./assets/steamlogowhite.png">
    </div>
    <div class="Dashboard justify-content-center">
      <Searchbar v-model="searchQuery" @submit="onSubmit"/>
      <div class="card-container justify-content-around" id="filterCardContainer">
        <div class="card shadow" id="filterCard">
          <div class="card-body text-white">
            <Advanced-search id="filterQuery" v-model="tagQuery" @click="filterTags" @filterInput="updateFilterInput" :title='titleTag' :options='tagOptions'/>
            <Advanced-search id="platformQuery" v-model="platformQuery" @click="filterPlatforms" @filterInput="updatePlatformInput" :title='titlePlatform' :options='platformOptions'/>
            <Advanced-search id="genreQuery" v-model="genreQuery" @click="filterGenres" @filterInput="updateGenreInput" :title='titleGenre' :options='genreOptions'/>
            <Advanced-search id="categoryQuery" v-model="categoryQuery" @click="filterCategories" @filterInput="updateCategoryInput" :title='titleCategory' :options='categoriesOptions'/>
            <div class="btn justify-content-center" id="filterButton" @click="filterTags">Apply Filter</div>
          </div>
        </div>
      </div>
      <Items :searchResults="searchResults"/>
    </div>
  </div>
</template>

<script>
import Searchbar from './components/Searchbar'
import AdvancedSearch from "@/components/AdvancedSearch";
import Items from "@/components/Items";
import axios from "axios";
import Vue from "vue";

export default {
  name: 'App',
  components: {
    Searchbar,
    AdvancedSearch,
    Items,
  },

  data() {
    return {
      searchQuery: '',
      searchResults: [],
      tagQuery: [],
      tagOptions: [],
      platformQuery: [],
      platformOptions: ['windows', 'mac', 'linux'],
      genreQuery: [],
      genreOptions: [],
      categoryQuery: [],
      categoriesOptions: [],
      titleTag: 'Filter Tags',
      titlePlatform: 'Filter Platforms',
      titleGenre: 'Filter Genres',
      titleCategory: 'Filter Categories',
    }
  },

  methods: {
    onSubmit() {
      axios.get(this.buildUrl()).then((response) => {
        if (response.data.searchResults === null) {
          this.searchResults = [];
        } else {
          this.searchResults = response.data.searchResults;
        }
      })
          .catch((error) => {
            console.log(error)
            this.searchResults = []
          })
    },
    buildUrl() {
      let url = 'http://ec2-44-193-104-82.compute-1.amazonaws.com:8080/api/search?';
      let tagString = ''
      let platformString = ''
      let genreString = ''
      let categoryString = ''

      if (this.searchQuery) {
        url += 'search=' + encodeURIComponent(this.searchQuery) + '&'
      }
      if (this.tagQuery.length !== 0) {
        tagString = 'tags=' + encodeURIComponent(this.tagQuery.join(',')) + '&'
      }
      if (this.platformQuery.length !== 0) {
        platformString = 'platforms=' + encodeURIComponent(this.platformQuery.join(',')) + '&'
      }
      if (this.genreQuery.length !== 0) {
        genreString = 'genres=' + encodeURIComponent(this.genreQuery.join(',')) + '&'
      }
      if (this.categoryQuery.length !== 0) {
        categoryString = 'categories=' + encodeURIComponent(this.categoryQuery.join(',')) + '&'
      }
      return url + tagString + platformString + genreString + categoryString
    },
    filterTags() {
      Vue.axios.get(this.buildUrl()).then((res) => {
        this.searchResults = res.data.searchResults;
      })
    },

    filterPlatforms() {
      Vue.axios.get(this.buildUrl()).then((res) => {
        this.searchResults = res.data.searchResults;
      })
    },

    filterGenres() {
      Vue.axios.get(this.buildUrl()).then((res) => {
        this.searchResults = res.data.searchResults;
      })
    },

    filterCategories() {
      Vue.axios.get(this.buildUrl()).then((res) => {
        this.searchResults = res.data.searchResults;
      })
    },

    updateFilterInput(newValue) {
      this.tagQuery = newValue
    },

    updatePlatformInput(newValue) {
      this.platformQuery = newValue
    },

    updateGenreInput(newValue) {
      this.genreQuery = newValue
    },

    updateCategoryInput(newValue) {
      this.categoryQuery = newValue
    },

  },

  mounted() {
    Vue.axios.get('http://ec2-44-193-104-82.compute-1.amazonaws.com:8080/api/tags').then((res) => {
      this.tagOptions = res.data.tags;
    });

    Vue.axios.get('http://ec2-44-193-104-82.compute-1.amazonaws.com:8080/api/categories').then((res) => {
      this.categoriesOptions = res.data.categories;
    });

    Vue.axios.get('http://ec2-44-193-104-82.compute-1.amazonaws.com:8080/api/genres').then((res) => {
      this.genreOptions = res.data.genres;
    });
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

#app {
  font-family: 'Roboto';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #1E1E24;
  padding-bottom: 450px;
}

.Dashboard {
  box-sizing: border-box;
  display: grid;
  align-content: center;
  margin-top: 50px;
  grid-template-rows: auto;
  grid-template-columns: auto;
}

.head{
  display: flex;
}

#mainCard{
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



#filterCard{
  background-color: #444140;
}

#filterCardContainer{
  float: right;
  grid-area: 1;
  grid-row: 1 / 3;
}

#filterButton{
  float: left;
  color: white;
  background-color: #644bde;
}

</style>
