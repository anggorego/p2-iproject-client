<template>
  <div>
    <div class="row flex"></div>
    <div>
    </div>
    <div>
    <Threads
    @threadDetailId="threadDetailId"
    ></Threads></div>
    <div></div>
  </div>
</template>
<script>
import Navbar from "../components/Navbar.vue"
import AddThread from "../components/addThread.vue"
import Threads from "../components/threads.vue"
import axios from 'axios'
export default {
  name:'Home',
  data() {
    return {
      threads:[],
      thread:{},
      user:''
    }
  },
  methods: {
    threadDetailId(page,thread){
      
      this.$emit('threadDetailId',page,thread)
    },
    fetchUser(){
      axios
        .get("http://localhost:3000/user",{
          headers:{
            access_token: localStorage.access_token
          }
        })
        .then(res=>{
          this.user = res.data.name
          this.$emit("userData",this.user)
        })
        .catch(err=>{
          console.log(err);
        })
    }
  },
  components:{
    Navbar,
    AddThread,
    Threads
  },
  created() {
    
    this.fetchUser()
  },
}
</script>