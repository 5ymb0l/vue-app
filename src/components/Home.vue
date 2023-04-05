<template>
    <Header />
    <h1> Hello {{ name }} Welcome Home</h1>
    <table class="center" border="1">
        <tr>
            <td> Id</td>
            <td> Name</td>
            <td> Contact</td>
            <td> Address</td>
            <td> Actions</td>

        </tr>
        <tr v-for="item in resturants" :key="item.id">
            <td> {{ item.id }}</td>
            <td> {{ item.name }}</td>
            <td> {{ item.contact }}</td>
            <td> {{ item.address }}</td>
            <td>
                <!-- <router-link :to = "'/update' + item.id">Update </router-link> -->
                <router-link  style="text-decoration: none; color: inherit;" :to="'/update/' + item.id"> Update </router-link>
                <button class="edit" v-on:click="deleteRestaurant(item.id)"> Delete </button>

            </td>

        </tr>
    </table>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name: "Home",
    data() {
        return {
            name: '',
            resturants: []
        }
    },
    components: {
        Header
    },
    methods: {
        async deleteRestaurant(id) 
        {
            let result = await axios.delete("http://localhost:3000/resturants/" + id);
            console.warn(result)
            if (result.status == 200) {
                 this.loadData()
            }
        },
        async loadData() 
        {
            let user = localStorage.getItem('user-info')
            this.name = JSON.parse(user).name;
            if (!user) {
                this.$router.push({ name: 'SignUp' })

            }
            let result = await axios.get("http://localhost:3000/resturants")
            // console.warn(result)
            this.resturants = result.data
        }

    },
     mounted() {
       this.loadData();
    }

}
</script>
<style>
td {
    width: 160px;
    height: 40px;
}
.center {
    margin-left: auto;
    margin-right: auto;
}
.edit  {
    cursor: pointer;
    background: coral;
    color: #fff;
    border: 1px solid coral;
    height: 40px;
    width: 100px;

}
</style>