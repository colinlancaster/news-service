<template>
  <div id="app">
    <h1>Status: {{ (status === "ok") ? "All well" : "Something is wrong" }}</h1>
    <h2>We've got {{ totalResults }} articles for your pleasure viewing</h2>
    <li v-for="article in articles" v-bind:key="article.title">{{ article.author ? article.author : "No Author Listed" }}</li>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function() {
    return {
      status: "",
      articles: [],
      totalResults: 0,
    }
    
  },
  mounted() {
    fetch("https://newsapi.org/v2/top-headlines?country=us&apiKey=c511282b17444f01bbd571a90aa24a1b")
      .then(response => response.json())
      .then((data) => {
        this.status = data.status;
        this.articles = data.articles;
        this.totalResults = data.totalResults;
      })
  },
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

h1, h2 {
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
