<template>
    <div>
        <h1>Customer Account</h1>
        <hr/>
        <h3> {{firstName}}'s Orders </h3>

        <p v-if="accountError" class="form-text text-danger">Can not get your account information, please try again later</p>
        
        <table v-if="reviewsByUser" class="table">
            <thead>
                <th>Order ID</th>
                <th>Order-Line IDFK</th>
                <th>Reward Points Awarded</th>
            </thead>
            <tbody>
                <tr v-for="thisOrder in ordersByCustomers" :key="thisOrder.OrderID">
                    <th><router-link :to="`/movies/${thisReview.MovieFK}`">{{thisReview.Title}}</router-link></th>
                    <th>{{thisReview.Summary}}</th>
                    <th>{{thisReview.Rating}}</th>
                </tr>
            </tbody>   
        </table>
    </div>
</template>


<script>
import axios from 'axios';

export default {
    data(){
        return{
            reviewsByUser: null,
            accountError: false
        }
    },
    computed:{
    firstName(){
        console.log(this.$store.state)
        return this.$store.state.user.NameFirst}
    },
    created(){
        axios.get("/reviews/me", {
            headers: {
                Authorization: `Bearer ${this.$store.state.token}`
            }
        })
        .then((response)=>{ 
            console.log("here is the reviews/me response:", response)
            this.reviewsByUser = response.data})
        .catch(()=>{
            this.accountError = true
        })
    }
}
</script>

<style scoped>

</style>