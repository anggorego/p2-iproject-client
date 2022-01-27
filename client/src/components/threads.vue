<template>
  <div>
    <table class="table table-hover w-auto">
  <thead>
    <tr>
      <th scope="col">title</th>
      <th scope="col">started by</th>
       <th scope="col"><i class="fas fa-reply"></i></th>
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
      <td>{{thread.Comments.length}}</td>
    </tr>
  </tbody>
</table>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  name:'Threads',
  data() {
    return {
      threads:[],

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
      
        this.threads = res.data
        })
        .catch(err=>{
        console.log(err);
        })
      },
 
    clickThreadDetail(thread){
      this.$emit("threadDetailId",'threadsDetail',thread)
    }
  },
  created() {
    this.fetchThreads()
  },
  components:{
    
  }
}
</script>