<template>
    <div>
        <h1>Customers</h1>
        <hr/>

        <table class="table">
            <thead>
                <tr>
                    <th>Customer ID</th>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>Email</th>
                    <th>Phone Number</th>
                    <th>Rewards ID</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="thisCustomer in Customers" :key="thisCustomer.CustomerID">
                    <th>{{thisCustomer.CustomerID}}</th>
                    <td>{{thisCustomer.NameFirst}}</td>
                    <td>{{thisCustomer.NameLast}}</td>
                    <td>{{thisCustomer.Email}}</td>
                    <td>{{thisCustomer.PhoneNumber}}</td>
                    <td>{{thisCustomer.RewardsIDFK}}</td>
                    <td>
                        <router-link :to="`/customers/${thisCustomer.CustomerID}`">
                            <button type="button" class="btn btn-primary">Customer Details</button>
                        </router-link>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
export default {
    computed:{
        movies(){return this.$store.state.customers}
    }
}
</script>

<style scoped>

</style>