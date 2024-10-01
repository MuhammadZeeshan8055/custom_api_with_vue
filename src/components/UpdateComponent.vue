<template>
    <div class="home-page-content">
        <h1>Update Restaurant Page</h1>
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
            <button type="button" v-on:click="updateRestaurant()">Update Restaurant</button>
        </form>
    </div>
</template>
<script>
import axios from 'axios';

export default{
    name:"UpdateComponent",

    data(){
        return{
            restaurant:{
                name:'',
                address:'',
                contact:''
            }
        }
    },
    async mounted(){
        let user=localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'LoginComponent'});
        }
        let result=await axios.get("http://localhost:3000/restaurant/"+this.$route.params.id);
        console.log(result.data);
        this.restaurant=result.data;
    },
    methods:{
        async updateRestaurant(){
            let result=await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact
            });
            if(result.status==200){
                alert('Restaurant Updated Successfully');
                this.$router.push({name:'Home'});

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
    }
</style>