<template> 
  <div id="app">
    <h1>{{ title }}</h1>

    <img alt="Vue logo" src="./assets/logo.png">
    
    <Navbar/>

    <main class="container py-5">

      <div class="alert alert-sussecss">
        Sono {{postList.length}} Risultati del Filtro:
        <br>
        {{printActiveFilters()}}
      </div>
        
      <div class="row row-cols-3 g-4">
        
        <div class="col" v-for="post in postList" :key="post.id">
          <PostCard 
            :title="post.title"
            :content="post.post"
            :img="post.cover_url"
            :tags="post.tags"
          />
        </div>

      </div>
    <main>

  </div>
</template>

<script>
import PostCard from "./components/PostCard.vue";
import Navbar from "./components/Navbar.vue";
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    //HelloWorld
    PostCard,
    Navbar,
  },

  data() {
    return {
      title: "La mia prima pagina con Vue cli",
      postsList: [],
      allPosts: [],
      datiFiltro: null,
      countFiltro: 0
    };
  },

  computed: {},
  methods: {
    onFilters(datiRicevuti) {
      this.postsList = datiRicevuti

      this.datiFiltro = datiRicevuti;
      this.countFiltro = datiRicevuti.results.length
    },

    printActiveFilters() {
      const toReturn = [];

      if(Object.keys(this.datiFiltro).length === 0) {
        return
      }

      for (const chiavefiltro of this.datiFiltro) {
        toReturn.push(chiave + " = " + this.datiFiltro[chiavefiltro]);
      }

      return toReturn.join("<br>");
    }
  },

  mounted() {
    this.axios.get("http://127.0.0.1:8000/api/posts")
    .then(resp =>{
      this.allPosts = resp.data.results;
      this.postsList = resp.data.results;
    })

    .catch(er =>{
      console.error(er)
      alert("Errore nel caricamento dei dati.")
    })
  }

};
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>