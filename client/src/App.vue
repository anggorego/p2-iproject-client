<template>
<div class="flex">
  <Navbar
  v-if="pageName == 'homePage' || pageName == 'threadsPage'|| pageName == 'threadsDetail'|| pageName == 'threadForm'"
  @directToThreadsList = "directToThreadsList"
  @backToHome = "backToHome"
  @backToLogin = "backToLogin"
  @directToPostThread = "directToPostThread"
  :userName = "user"
  ></Navbar>
  <Register
  v-if="pageName == 'registerPage'"
  @directToLogin = "directToLogin"
  @directToHome = "directToHome"
  ></Register>
  <Login
  @directToHome = "directToHome"
   v-else-if="pageName == 'loginPage'"
  ></Login>
  <Home
  v-else-if="pageName == 'homePage'"
  @threadDetailId="threadDetailId"
  @userData="userData"
  ></Home>
  <ThreadPage
  v-else-if="pageName == 'threadsPage'"
  @threadDetailIdThread="threadDetailIdThread"
  ></ThreadPage>
  <ThreadDetail
  v-else-if="pageName == 'threadsDetail'"
  :threadDetailId = "thread"
  :threadDetailIdThreadPage = "threadfromthreadPage"
  @backToHome="backToHome"
  ></ThreadDetail>
  <ThreadForm
  v-else-if="pageName == 'threadForm'"
  @afterPostThread = "afterPostThread"
  ></ThreadForm>
</div>
</template>
<script>

import Login from "./views/Login.vue"
import Register from "./views/RegisterPage.vue"
import Home from "./views/Home.vue"
import ThreadPage from "./views/ThreadPage.vue"
import Navbar from './components/Navbar.vue'
import ThreadDetail from "./views/Threaddetail.vue"
import ThreadForm from "./views/ThreadForm.vue"

export default {
  name:'App',
  data() {
    return {
      pageName: 'registerPage',
      thread :{},
      user:'',
      threadfromthreadPage:{}
    }
  },
  methods: {
    directToHome(page){
      if(localStorage.access_token){
        this.pageName = page
      }
    },
    directToLogin(page){
      this.pageName = page
    },
    backToLogin(page){
        localStorage.clear()
        this.pageName = page
    },
    directToThreadsList(page){
      this.pageName = page
    },
    threadDetailId(page,thread){
      // console.log(thread,'yang ini');
      this.pageName = page
      this.thread = thread
    },
    backToHome(page){
      this.pageName = page
    },
    directToPostThread(page){
      this.pageName = page
    },
    afterPostThread(page){
      this.pageName = page
    },
    userData(data){
      this.user = data
    },
    threadDetailIdThread(page,thread){
      this.pageName=page
      console.log(thread,'ini yg dimasksu');
      this.thread=thread
    }
  },
  components:{
    Register,
    Login,
    Home,
    ThreadPage,
    Navbar,
    ThreadDetail,
    ThreadForm
  },
  created() {
    if(localStorage.access_token){
      this.pageName = 'homePage'
    }
  },
}
</script>