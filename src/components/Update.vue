<template>
    <Header />
    <h1 class="font-bold text-3xl p-2 my-10">Welcome to Update Book</h1>
    <div class="flex-col flex-wrap">
        <h1 class="text-4xl font-bold mb-[20px] p-2">Update Book</h1>
        <div class="inputs">
            <input id="name" class="pl-[20px]" type="text" placeholder="Enter Name" autocomplete="off"
                v-model="book.name">
        </div>
        <div class="inputs">
            <input id="author" class="pl-[20px]" type="text" placeholder="Enter Author" autocomplete="off"
                v-model="book.author">
        </div>
        <div class="inputs">
            <input id="rating" class="pl-[20px]" type="text" placeholder="Enter Rating" autocomplete="off"
                v-model="book.rating">
        </div>
        <button @click="updateResturant" class="btn-primary">Update</button>
    </div>
</template>

<script>

import axios from 'axios'
import Header from './Header.vue';

export default {
    name: "my-update",
    components: {
        Header
    },
    data() {
        return {
            book: {
                name: "",
                author: "",
                rating: ""
            }
        }
    },
    methods:{
        async updateResturant(){
            let newBook = {
                "name" : this.book.name,
                "rating" : this.book.rating,
                "author" : this.book.author
            }
            let result = await axios.put("https://booback.onrender.com/books/"+this.$route.params.id, newBook)
            if(result.status==200){
                this.$router.push({name: "Home"})
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem("user-info")
        if (user == null) {
            this.$router.push({ name: 'Signup' })
        }
        let result = await axios.get(`https://booback.onrender.com/books?_id=${this.$route.params.id}`)
        this.book = result.data[0]
    },
}

</script>