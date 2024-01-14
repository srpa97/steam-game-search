<template>
  <div class="searchbar">
      <div class="form-outline" id="searchBar">
        <b-form-input v-on:keypress.enter="onSubmit" id="form1" class="form-control rounded-pill" placeholder="Search for game"
               aria-label="Search" :value="value" @input="onQueryInput"/>
        <button v-on:click="onSubmit" type="button" id="button1" class="btn rounded-pill">Search</button>
      </div>
  </div>
</template>

<script>
import AdvancedSearch from "@/components/AdvancedSearch";

export default {
  props: {
    value: String
  },

  methods:{
    onSubmit(event) {
      event.preventDefault();
      this.$emit('submit');
      AdvancedSearch.data().value.splice(0)
    },
    onQueryInput(event){
      this.$emit('input', event)
    }
  }
}
</script>

<style scoped>

.searchbar{
  margin-left: 10px;
  margin-bottom: 20px;
  grid-column: 2;
}

#form1{
  width: 472px;
  float: left;
  margin-right: 5px;
}

#button1{
  float: left;
  color: white;
  background-color: #644bde;
}


</style>