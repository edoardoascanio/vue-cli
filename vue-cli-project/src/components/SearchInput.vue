<template>

    <form class="d-flex" @submit.prevent="onSubmit">
        <input 
        class="form-control me-2"
        type="search"
        placeholder="Search"
        aria-label="Search"
        />

        <button class="btn btn-outline-primary">Search</button>  
    </form>

</template>

<script>
export default {
    name:"SearchInput",
    data() {
        return {
            searchData: "",
        };
    },
    methods:{
        onsubmit(){
            this.axios.get("http://127.0.0.1:8000/api/posts/filter", {
                params: {
                    content: this.searchData
                }
            }).then(resp => {
                this.$emit("filters", resp.data)
            })
            .catch(er =>{
                console.error(er);
                alert("Errore filtraggio dati")
            });
        }
    }
};
</script>