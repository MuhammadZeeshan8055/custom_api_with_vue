<template>
    <div class="home-page-content">
        <h1>Add Restaurant Page</h1>
        <form>
            <input type="text" name="" id="" placeholder="Enter Restaurant Name" v-model="restaurant.name">
            <br>
            <br>
            <input type="text" name="" id="" placeholder="Enter Restaurant Address" v-model="restaurant.address">
            <br>
            <br>
            <input type="text" name="" id="" placeholder="Enter Restaurant Contact" v-model="restaurant.contact">
            <br>
            <br>
            <button type="button" v-on:click="addRestaurant()">Add Restaurant</button>
        </form>
    </div>
</template>
<script>
import axios from 'axios';

export default{
    name:"AddComponent",

    data(){
        return{
            restaurant:{
                name:'',
                address:'',
                contact:''
            }
        }
    },
    
    mounted(){
        let user=localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'LoginComponent'});
        }
    },

    methods:{
        async addRestaurant(){
            let result=await axios.post("http://localhost:3000/restaurant",{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact
            });
            if(result.status==201){
                alert('Restaurant Added Successfully');
                this.restaurant.name = '';
                this.restaurant.address = '';
                this.restaurant.contact = '';
            }
        }
    }

}
</script>

<style>
    .home-page-content{
       display: flex;
       justify-content: center;
       margin-top: 10%;
       flex-direction: column;
    }
</style>