<template>
    <nav class="navbar navbar-expand-md navbar-dark bg-dark shadow-sm">
        <div class="container">
            <a class="navbar-brand" href="">
                VUE
            </a>
    
            <div class="nav-item">
                <a class="nav-link" href="">
                    Visita il sito
                </a>

                <a class="nav-link" href="">
                    Logout
                </a>
            </div>

            <SearchInput @filters="onFilters"/>
        </div>
    </nav>
</template>
 
<script>
import SearchInput from "./SearchInput.vue";

export default {
    name: "Navbar",
    components: {
        SearchInput,
    },

    methods: {
        onFilters(datiInviatiDalEmit) {
            this.$emit("filters", datiInviatiDalEmit)
        }
    }
};
</script>