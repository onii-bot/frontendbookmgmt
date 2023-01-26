<template>
<Header/>
<h1 class="font-bold text-3xl p-2 my-10">Welcome to add</h1>
<div class="flex-col flex-wrap">
    <h1 class="text-4xl font-bold mb-[20px] p-2">Add Book</h1>
    <div class="inputs">
        <input id="name" class="pl-[20px]" type="text" placeholder="Enter Name" autocomplete="off" v-model="name">
    </div>
    <div class="inputs">
        <input id="author" class="pl-[20px]" type="text" placeholder="Enter Author" autocomplete="off" v-model="author">
    </div>
    <div class="inputs">
        <input id="rating" class="pl-[20px]" type="text" placeholder="Enter Rating" autocomplete="off" v-model="rating">
    </div>
    <button @click="submitBook" class="btn-primary">Submit</button>
</div>
</template>

<script>

import axios from 'axios';
import Header from './Header.vue';


export default{
    name: "my-add",
    components: {
        Header
    },
    data(){
        return{
            name : "",
            author : "",
            rating : ""
        }
    },
    methods: {
        async submitBook(){
            let newBook = {
                "name" : this.name,
                "rating" : this.rating,
                "author" : this.author
            }

            let result = await axios.post("https://backendforbookmg.herokuapp.com/books", newBook)
            if(result.data.status==201){
                this.$router.push({name: "Home"})
            }
        }
    },
    mounted(){
        let user = localStorage.getItem("user-info")
        if(user==null){
            this.$router.push({name: 'Signup'})
        }
    }
}

</script>