<template>
<img class="logo" alt="logo" src="../assets/logo.png">
<div class="flex-col flex-wrap">
    <h1 class="text-4xl font-bold mb-[20px] p-2">Login</h1>
    <div class="inputs">
        <input id="email" class="pl-[20px]" type="text" placeholder="Enter Email" autocomplete="off" v-model="email">
    </div>
    <div class="inputs">
        <input id="password" class="pl-[20px]" type="password" placeholder="Enter Password" autocomplete="off" v-model="password">
    </div>
    <button @click="login" class="btn-primary">Login</button>
    
</div>
<p class="mt-[16px] py-2 px-4 hover:underline">
<router-link to="/signup">Signup</router-link>  
</p>
</template>
    
<script>

import axios from 'axios';

export default{
    name: "my-login",
    data(){
        return{
            email : "",
            password : ""
        }
    },
    methods: {
        async login(){
            let result = await axios.get(`https://backendforbookmg.herokuapp.com/users?email=${this.email}&password=${this.password}`)
            if(result.status==200 && result.data.length>0){
                localStorage.setItem("user-info",JSON.stringify(result.data[0]));
                this.$router.push({name: 'Home'})
            }
        }
    },
    mounted(){
        let user = localStorage.getItem("user-info");
        if(user){
            this.$router.push({name: 'Home'})
        }
    },

}

</script>
