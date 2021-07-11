<template>
    <div class="card" style="width: 18rem;">
        <img src="" class="card-img-top" alt="" />
        <div class="card-body">
            <h5 :class="titleClass" class="card-title">{{title}}</h5>

            <p class="card-text" v-html="content"></p>
            
            <a href="#" @click="onLinkClick" class="btn btn-primary">{{linkText}}</a>
        </div>
    </div> 
</template>

<script>
export default {
    name: "PostCard",
    props: {
        title: {
            type:String,
            required: true
        },
        content: String,
        linkText:{
           type: String,
           default: "Mostra dettagli"
        },
        img: String,
    },
    
    data() {
        return {
            variabile1: ""
        }
    },

    methods: {
        onLinkClick() {
            alert(this.title)
        }
    }
};
</script>
