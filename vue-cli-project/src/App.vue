<template> 
  <div id="app">
    <h1>{{ title }}</h1>

    <img alt="Vue logo" src="./assets/logo.png">
    
    <Navbar/>

    <div class="container py-5">
      
      <TextInput label="input di prova" v-model="textInputValue"/>
      <TextAreaInput label="input di prova" v-model="textInputValue"/>

      <div class="alert alert-sussecss">
        Sono {{postList.length}} Risultati del Filtro:
        <br>
        <div v-html="printActiveFilters()"></div>

        <br>
        <a href="#" class="btn btn-link" @click="resetFilter">Annulla filtri </a>
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
    </div>

  </div>
</template>

<script>
import PostCard from "./components/PostCard.vue";
import Navbar from "./components/Navbar.vue";
import TextInput from "./components/TextInput.vue";
import TextAreaInput from "./components/TextAreaInput.vue";
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    //HelloWorld
    PostCard,
    Navbar,
    TextInput,
    TextAreaInput,
  },

  data() {
    return {
      title: "La mia prima pagina con Vue cli",
      postsList: [],
      allPosts: [],
      datiFiltro: null,
      countFiltro: 0,
      textInputValue: ""
    };
  },

  computed: {},
  methods: {
    onFilters(datiRicevuti) {
      const searchedContent = datiRicevuti.filters.content;

      this.postsList = datiRicevuti.results.map(post => {
        const esprReg = new RegExp(searchedContent, "g");

        post.content = post.content.replace(esprReg, 
        `<span class="marked">${searchedContent}</span>`)

        return post;
      });

      this.datiFiltro = datiRicevuti;
      this.countFiltro = datiRicevuti.results.length
    },

    printActiveFilters() {
      const toReturn = [];

      if(Object.keys(this.datiFiltro).length === 0) {
        return
      }

      for (const chiavefiltro of this.datiFiltro) {
        toReturn.push(chiavefiltro + " = " + this.datiFiltro[chiavefiltro]);
      }

      return toReturn.join("<br>");
    },

    resetFilter() {
      this.postsList = this.allPosts
      this.datiFiltro = null
      this.countFiltro = 0
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

.marked{
  background-color: yellow ;
}
</style>