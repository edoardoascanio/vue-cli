<template> 
  <div id="app">
    <h1>{{ title }}</h1>

    <img alt="Vue logo" src="./assets/logo.png">
    
    <Navbar/>

    <main class="container">
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
      postList: [],
    };
  },

  computed: {},
  methods: {},

  mounted() {
    this.axios.get("http://127.0.0.1:8000/api/posts")
    .then(resp =>{
      this.postList = resp.data.results;
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