<template>

    <form class="d-flex" @submit.prevent="onSubmit">
        <input 
        class="form-control me-2"
        type="search"
        placeholder="Search"
        aria-label="Search"
        />
        
        <select class="form-select" v-model="searchTag">
            <option v-for="tag in tagList" :key="tag.id" :value="tag.id">
                {{tag.name}}
            </option>
        </select>
        <button class="btn btn-outline-primary">Search</button>  
    </form>

</template>

<script>
export default {
    name:"SearchInput",
    data() {
        return {
            searchData: "",
            searchTag: "",
            tagList: [],
        };
    },
    methods:{
        onsubmit(){
            this.axios.get("http://127.0.0.1:8000/api/posts/filter", {
                params: {
                    content: this.searchData,
                    tags: this.searchTag
                }
            }).then(resp => {
                this.$emit("filters", resp.data)
            })
            .catch(er =>{
                console.error(er);
                alert("Errore filtraggio dati")
            });
        }
    },

    mounted() {
        this.axios.get("http://127.0.0.1:8000/api/tags")
            .then(resp => {
               this.tagList = resp.data.results;
            })
            .catch(er => {
                console.error(er);

                alert("Non posso recuperare i tags")
            });
    }

};
</script>