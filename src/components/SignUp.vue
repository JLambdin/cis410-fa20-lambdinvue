<template>
    <div>
        <h1>Sign Up</h1>
        <form @submit.prevent="onSubmit">
            <div class="form-group"><label for="fname-input">First name</label> <input type="text" id="fname-input" required="required" placeholder="First name" class="form-control" v-model="NameFirst"></div> 
            
            <div class="form-group"><label for="lname-input">Last name</label> <input type="text" id="lname-input" required="required" placeholder="Last name" class="form-control" v-model="NameLast"></div> 
            
            <div class="form-group"><label for="email-input">Email address</label> <input type="email" id="email-input" required="required" placeholder="Enter email" class="form-control" v-model="Email"> 
            <small v-if="dupEmail" class="from-text text-danger">Please chose a different email.</small>
            </div> 

            <div class="form-group"><label for="phone-input">Phone Number</label> <input type="text" id="phone-input" required="required" placeholder="Phone Number" class="form-control" v-model="PhoneNumber"></div> 

       
            
            <div class="form-group"><label for="password-input">Email Password</label> <input type="password" id="password-input" placeholder="Password" required="required" value="asdfasdf" class="form-control" v-model="EmailPassword">
            
            </div> <button type="submit" class="btn btn-primary">Submit</button> <p id="error-signup" class="text-danger">{{errorMessage}}</p>
            
            </form>
    </div>
</template>


<script>
import axios from 'axios';

export default {
    data(){
        return {
            NameFirst:'',
            NameLast: '',
            Email:'',
            PhoneNumber:'',
            EmailPassword:'',
            errorMessage:'',
            dupEmail: false
        }
    },
    methods:{
        onSubmit(){

            const myFormData = {
                NameFirst: this.NameFirst,
                NameLast: this.NameLast,
                Email: this.email,
                PhoneNumber: this.NameLast,
                EmailPassword: this.password
            }
            // console.log(myFormData)

            axios.post("/customers", myFormData)
                .then((myResponse)=>{
                    // console.log(myResponse)
                    this.$router.replace("/signin?signupsuccess=true")
                    })
                .catch((myError)=>{
                    if(myError.response.status === 409){
                        this.dupEmail = true
                    }else{
                        this.errorMessage = "Cannot sign you up, please try again later."
                    }

                })
        }
    }
}
</script>

<style scoped>

</style>