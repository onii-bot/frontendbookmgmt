<template>
    <div class="flex justify-around space-x-44 text-base bg-purple-800 text-white">
        <router-link class="p-3 hover:text-purple-900 hover:bg-white cursor-pointer" to="/">Home</router-link>
        <router-link class="p-3 hover:text-purple-900 hover:bg-white cursor-pointer" to="/add">Add Book</router-link>
        <a @click="logout" class="p-3 mr-2 hover:text-purple-900 hover:bg-white cursor-pointer">Log out</a>
    </div>
</template>

<script>
export default{
    name: "my-header",
    methods: {
        logout(){
            localStorage.clear()
            this.$router.push({name: "Login"})
        }
    }
}
</script>
