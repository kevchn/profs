<template>
  <div id="app">
    <div class="container">
      <h1 class="title">
        UMD CS Professors
      </h1>
      <p class="subtitle">
        A way to find UMD CS <strong>Professors</strong>!
      </p>

      {{ info }}

      <directory></directory>

      <div>
        <a href="https://www.semanticscholar.org/">Semantic Scholar</a>
        <a href="https://www.semanticscholar.org/">Semantic Scholar</a>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Directory from './components/Directory.vue'

export default {
  name: 'App',

  components: {
    Directory
  },

  data: function() {
    return {
      professors: [],
      info: "Default"
    }
  },

  created() {
    axios.get(`https://cors.io/?http://api.umd.io/v0/professors?departments=CMSC&semester=201805`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.professors = response.data
    })
    .catch(e => {
      this.errors.push(e)
    }),

    umd = rmp("University of Maryland")

    this.info = umd.get("Thomas Goldstein", function(professor) {
      if (professor === null) {
        this.info = "IDK"
      } else {
        this.info = professor
      }
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
