<template>
  <div class="row mt-5">
      <form>
    <fieldset>
      <legend>REGISTER FORM</legend>
      <div class="form-group">
        <label for="exampleInputPassword1" class="form-label mt-4">Full Name</label>
        <input type="text" class="form-control" id="exampleInputPassword1" placeholder="full name"
        v-model="nameRegister"
        >
        <label for="exampleInputEmail1" class="form-label mt-4">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email"
        v-model="emailRegister"
        >
        <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
        <label for="exampleInputPassword1" class="form-label mt-4">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password"
        v-model="passwordRegister"
        >
        <label for="exampleInputPassword1" class="form-label mt-4">Phone Number</label>
        <input type="number" class="form-control" id="exampleInputPassword1" placeholder="Phone Number"
        v-model="phoneRegister"
        >
      </div>
      <button type="submit" class="btn btn-secondary"
      @click.prevent="clickButtonRegister"
      >Submit</button>
    </fieldset>
      <p class="mt-3"> already have an account ? </p> 
     <button type="submit" class="btn btn-secondary"
      @click.prevent="clickButtonLoginRegister"
      >login here</button>
  </form>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Register',
  data() {
    return {
      nameRegister:'',
      emailRegister:'',
      passwordRegister:'',
      phoneRegister:''
    }
  },
  methods: {
    clickButtonRegister(){
      axios
           .post("http://localhost:3000/register",{
              name: this.nameRegister,
              email: this.emailRegister,
              password: this.passwordRegister,
              phoneNumber: this.phoneRegister,
            })
            .then(({data})=>{
              swal({
              title: "SUCCESS",
              text: "Please click `Login Here` to login",
              icon: "success",
              });
               this.$emit("directToLogin", "loginPage")
            })
            .catch((err)=>{
              console.log(err);
              swal({
                title: "FAILED",
                icon: "error",
              });
            })
    },
    clickButtonLoginRegister(){
        this.$emit("directToLogin", "loginPage")
        // this.isRegister = true
        // this.isLogin = true
    },
  },
}
</script>