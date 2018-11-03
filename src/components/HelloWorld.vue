<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input 
      v-model="searchTerm"
      class="input" 
      type="text"
      name="search" 
    >
    <button 
      class="button is-primary is-large"
      @click="performSearch"
    >Search</button>
    <div class="myContent"><img 
      v-for="i in images" 
      :key="i.id" 
      :src="i.images.fixed_height.url"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
import "../../node_modules/bulma/css/bulma.css";
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Image Search Manipulator",
      searchTerm: "",
      images: []
    };
  },
  methods: {
    performSearch() {
      const link =
        "http://api.giphy.com/v1/gifs/search?api_key=dc6zaTOxFJmzC&limit=5&q=";
      const apiLink = link + this.searchTerm;
      axios
        .get(apiLink)
        .then(response => {
          console.log(response);
          this.images = response.data.data;
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.myContent {
  padding-top: 20px;
}
img {
  padding: 5px;
}
</style>
