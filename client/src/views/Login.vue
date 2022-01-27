<template>
  <div class="row mt-5">
     <form>
    <fieldset>
      <legend>LOG IN HERE</legend>
      <div class="form-group">
        <label for="exampleInputEmail1" class="form-label mt-4">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email"
        v-model="emailLogin"
        >
        <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
        <label for="exampleInputPassword1" class="form-label mt-4">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password"
        v-model="passwordLogin"
        >
      </div>
      <button type="submit" class="btn btn-secondary"
      @click.prevent="clickButtonLogin"
      >Submit</button>
    </fieldset>
    <p class="mt-4">Don't have an account yet ?</p>
     <button type="submit" class="btn btn-secondary mb-2"
      @click.prevent="clickButtonRegisterLogin"
      >register here</button>
  </form>
    
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name:'Login',
  data() {
    return {
      emailLogin:'',
      passwordLogin:''
    }
  },
  methods: {
    clickButtonLogin(){
        if(!this.emailLogin || !this.passwordLogin){
           swal({
              title: "FAILED",
              text:"Invalid email/password",
              icon: "error",
            });
        }
      axios
      .post("http://localhost:3000/login",{
            email:this.emailLogin,
            password:this.passwordLogin
      })
      .then(({data})=>{
          swal({
            title: "SUCCESS",
            text: "Logged in",
            icon: "success",
          });
        localStorage.setItem('access_token',data.access_token)
        this.$emit("directToHome","homePage")
     
        })
        .catch((err)=>{
            swal({
              title: "FAILED",
              text:"Invalid email/password",
              icon: "error",
            });
        })
    },
    clickButtonRegisterLogin(){
       this.$emit("directToRegister", "registerPage")
    }
  },
}
</script>