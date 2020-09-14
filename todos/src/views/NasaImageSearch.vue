<template>
  <div class="nasaimagesearch">
    <h2>Search for NASA Images</h2>
    <!-- <button type="button" class="btn btn-primary">Primary</button> -->
    <div class="col-md-4 offset-md-4 mt-5 border border-success pt-3">
      <div class="input-group mb-3">
        <input type="text" class="form-control" placeholder="Search ......" aria-label="Recipient's username" v-model="query">
        <div class="input-group-append" @click="getResults(query)">
          <span class="input-group-text"><i class="fa fa-search"></i></span>
        </div>
      </div>
    </div>

    <div v-if="results">
      <div v-for="result in results" :key="result.id">
        <img :src="result.links[0].href"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'NasaImageSearch',
  components: {
    
  },
  data() {
    return {
      query: '',
      results: ''
    }
  },
  methods: {
    getResults(query) {
      axios.get('https://images-api.nasa.gov/search?q='+query+'&media_type=image').then((response) => {
  console.log(response.data.collection.items);
  this.results = response.data.collection.items;

})
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
@import'../../node_modules/bootstrap/dist/css/bootstrap.css';
@import '../../node_modules/font-awesome/css/font-awesome.css';
</style>