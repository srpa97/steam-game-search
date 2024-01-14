<template>
  <div class="advancedSearch">
          <a>{{ title }}</a>
          <multiselect id="menu" v-model="value" :select="filterTags" :options="options" :multiple="true" :close-on-select="false">
            <template slot="selection" slot-scope="{ values, search, isOpen }"><span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">{{ values.length }} options selected</span></template>
          </multiselect>
<!--          <div class="btn-danger rounded-pill justify-content-center" v-on:click="filterTags">Apply Filter</div>-->
  </div>
</template>

<script>

import 'bootstrap/dist/js/bootstrap.bundle';
import Multiselect from 'vue-multiselect'
import Vue from "vue";

Vue.component('multiselect', Multiselect)

export default {
  props: {
    title: String,
    options: []
  },
  data() {
    return {
      value: []
    }
  },
  mounted() {
    // Vue.axios.get('http://localhost:8080/api/tags').then((res) => {
    //   this.options = res.data.tags;
    //   //console.warn(res.data.tags)
    // });
  },

  methods:{
    filterTags(event) {
      event.preventDefault();
      this.$emit('click', this.value);
    },
    emitEventChanged () {
      this.$emit('CustomEventInputChanged', this.value);
    },
    onfilterInput() {
      this.$emit('filterInput', this.value)
    }
  },
  watch: {
    value: function (){
      this.onfilterInput()
    }
  }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<style scoped>

.advancedSearch{
  grid-column: 4;
}

.multiselect{
  width: 250px;
  margin-bottom: 20px;
}

</style>