<template> 
  <div id="app">
    <h1>{{ title }}</h1>

    <img alt="Vue logo" src="./assets/logo.png">
    
    <Navbar/>

    <div class="container">
      <div class="row row-cols-3 g-4">
        <div class="col" v-for="index in 10" :key="index">
          <PostCard 
            :title="'Titolo' + index"
            :content="'Contenuto della card' + index"
            :linkText="'Mostra dettagli'"
          />
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import PostCard from './components/PostCard.vue';
import Navbar from './components/Navbar.vue';
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    //HelloWorld
    PostCard,
    Navbar,
  },

  data() {
    return {
      title: "La mia prima pagina con Vue cli"
    }
  },

  computed:{

  },

  methods:{

  },

}
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