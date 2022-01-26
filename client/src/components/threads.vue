<template>
  <div>
    <table class="table table-hover">
  <thead>
    <tr>
      <th scope="col">title</th>
      <th scope="col">started by</th>
    </tr>
  </thead>
  <tbody>
    <tr class="table-dark"
       v-for="thread in threads"
      :key="thread.id"
      @click="clickThreadDetail(thread)"
      >
      <th scope="row">
        {{thread.title}}
        </th>
      <td>{{thread.User.name}}</td>
    </tr>
  </tbody>
</table>
  </div>
</template>
<script>
import axios from 'axios'
import Navbar from "../components/Navbar.vue"
export default {
  name:'Threads',
  data() {
    return {
      threads:[]
    }
  },
   methods: {
    fetchThreads(){
    axios
      .get("http://localhost:3000/threads",{
          headers:{
            access_token: localStorage.access_token
          }
        })
        .then(res=>{
        //  console.log(res.data);
        this.threads = res.data
        })
        .catch(err=>{
        console.log(err);
        })
      },
    clickThreadDetail(thread){
      // console.log(thread,'ihi dari mythread');
      this.$emit("threadDetailId",'threadsDetail',thread)
    }
  },
  created() {
    this.fetchThreads()
  },
  components:{
    Navbar
  }
}
</script>