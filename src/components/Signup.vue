<template>
<img class="logo" alt="logo" src="../assets/logo.png">
<div class="flex-col flex-wrap">
    <h1 class="text-4xl font-bold mb-[20px] p-2">Sign up</h1>
    <div class="inputs">
        <input id="name" class="pl-[20px]" type="text" placeholder="Enter Name" autocomplete="off" v-model="name">
    </div>
    <div class="inputs">
        <input id="email" class="pl-[20px]" type="text" placeholder="Enter Email" autocomplete="off" v-model="email">
    </div>
    <div class="inputs">
        <input id="password" class="pl-[20px]" type="password" placeholder="Enter Password" autocomplete="off" v-model="password">
    </div>
    <button @click="submitForm" class="btn-primary">Signup</button>
    
</div>
<p class="mt-[16px] py-2 px-4 hover:underline">
    <router-link to="/login">Login</router-link>  
    </p> 
</template>

<script>

import axios from 'axios';

export default{
    name: "my-signup",
    data(){
        return{
            name : "",
            email : "",
            password : ""
        }
    },
    methods: {
        async submitForm(){
            if(this.name==="" || this.email==="" || this.password===""){
                alert("fill")
                return
            }
            let form = {
                "name" : this.name,
                "email" : this.email,
                "password" : this.password
            }
            let result = await axios.post("https://booback.onrender.com/users",form)
            if(result.data.status == 201){
                localStorage.setItem("user-info", JSON.stringify(form))
                this.$router.push({name: 'Home'})
            }
            
        }
    },
    mounted(){
        let user = localStorage.getItem("user-info")
        if(user){
            this.$router.push({name: 'Home'})
        }
    },
}

</script>

<style>

.logo {
    width: 100px;
    margin: auto;
}

input {
    border: 2px solid black;
    width: 400px;
    height: 60px;

}

.inputs {
    padding-left: 20px;
    margin-bottom: 25px;
}

</style>