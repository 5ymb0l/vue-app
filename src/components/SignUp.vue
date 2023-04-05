<template>
<img  class ="logo" src="../assets/the-red-cafe.png">
<h1> Sign Up </h1>
<div class="register">
  <input type="text" v-model="name" placeholder="Enter Name" />
  <input type="text" v-model="email" placeholder="Enter Email" />  
  <input type="password" v-model="password" placeholder="Enter Password" />  
  <button v-on:click="signUp"> Sign Up</button>
  <p> 
    <router-link to = "/login">
      Login
    </router-link>
  </p>
</div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'SignUp',
    data() {
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods : {
     async signUp()
        {
            let result =  await axios.post("http://localhost:3000/users", {
                email : this.email,
                password : this.password,
                name: this.name
            });
            // console.warn("signUp" , this.name ,this.email,this.password)
            console.log(result);
            if (result.status == 201) {
                // alert("signUp Success")
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name: 'Home'})
            }
        }
    }, 
       mounted() { // this method is used when the user is on the home page he can't redirect to login/singup page
          let user = localStorage.getItem('user-info')
          if(user)
           {
            this.$router.push({name: 'Home'})

          }
       }
}
</script>
<style>

</style>