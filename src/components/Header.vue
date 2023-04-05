<template> 
<div class="nav">
   
<router-link to="/"> Home</router-link>
<router-link to="/add"> Add Res</router-link>
<router-link to="/update"> Update Res</router-link>

<a v-on:click="logout" href="#"> Logout</a>


</div>
</template>
<script>
export default {
    name : 'Header',
    methods:{
        logout()
        {
            localStorage.clear();
            this.$router.push({name : ''})
        }
    }
}
</script>
<style>
.nav{
background-color: #333;
overflow: hidden;
}
.nav a {
    float: left;
    color: white;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
  background: #ddd;
  color: #333;
}
</style>