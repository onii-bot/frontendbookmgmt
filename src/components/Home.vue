<template>
<Header />
<h1 class="my-10">Welcome {{ name }}</h1>

<div class="relative overflow-x-auto">
    <table class="text-sm text-black w-[800px] text-center mx-auto">
        <thead class="text-xs text-black uppercase bg-purple-200 ">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Id
                </th>
                <th scope="col" class="px-6 py-3">
                    Name
                </th>
                <th scope="col" class="px-6 py-3">
                    Author
                </th>
                <th scope="col" class="px-6 py-3">
                    Rating
                </th>
                <th scope="col" class="px-6 py-3">
                    Actions
                </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(item, index) in books" :key="item.id" class="bg-white border-b">
                <th scope="row" class="px-6 py-4 font-medium text-black whitespace-nowrap">
                    {{index+1}}
                </th>
                <td class="px-6 py-4">
                    {{item.name}}
                </td>
                <td class="px-6 py-4">
                    {{item.author}}
                </td>
                <td class="px-6 py-4">
                    {{item.rating}}
                </td>
                <td class="px-6 py-4">
                    <router-link class="border border-1 border-black rounded-sm p-1 mx-1 text-sm text-purple-400 hover:bg-purple-400 hover:text-black" :to="'/update/'+item._id">Update</router-link>
                    <!-- <button class="border border-1 border-black rounded-sm py-[0.15rem] pl-1 pr-[0.4rem] mx-1 text-sm text-purple-400 hover:bg-purple-400 hover:text-black" @click="deleteBook(item._id)">Delete</button> -->
                </td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>

import axios from 'axios'
import Header from './Header.vue'

export default{
    name: "my-home",
    components: {
        Header
    },
    data(){
        return{
            name : "",
            books : [],
            index : 0
        }
    },
    methods:{
        async deleteBook(id){
            let result_books = await axios.delete("https://backendforbookmg.herokuapp.com/books/"+id)
            if(result_books.status==200){
                this.loadData()
            }
        },

        async loadData(){
            let result_books = await axios.get("https://backendforbookmg.herokuapp.com/books")
            this.books = result_books.data
        }
    },
    mounted(){
        let user = localStorage.getItem("user-info")
        if(user==null){
            this.$router.push({name: 'Signup'})
        }
        let data = JSON.parse(user)
        this.name = data.name
        this.loadData()
    }
}
</script>