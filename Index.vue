<template>
  <div id="app"> 
    <h1>{{msg}}i</h1>
    <div v-if="loading">Loading...</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Flashcards",
  data() {
    return {
      msg: "Flashcards!",
      items: null,
      loading: true,
      errored: false,
      errormsg: null
    };
  },
  mounted () {
    axios
      .get('https://arcane-journey-69138.herokuapp.com/cards/all')
      .then(response => {
        this.items = response.data        
      })
      .catch(error => {
        this.errored = true
        this.errormsg = error
      })
      .finally(() => this.loading = false)
  }
};
</script>

<style scoped>
#app {
      font-family: "Avenir", Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
          -moz-osx-font-smoothing: grayscale;
            text-align: center;
              color: #2c3e50;
                       margin-top: 60px;
}
h1,h2 {
  font-weight: normal;
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
  color: #42b983;
}
</style>
