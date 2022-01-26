<template>
<div>
  <div>
  <table class="table table-hover">
  <thead>
      <tr>
      <th scope="col">title</th>
      <th scope="col">description</th>
    </tr>
  </thead>
  <tbody>
    <tr class="table-dark"
       v-for="thread in threads"
      :key="thread.id"
      @click="clickThreadDetailfromThreadPage(thread)"
      >
      
      <th scope="row">
        {{thread.title}}
        </th>
      <td>{{thread.description}}</td>
  </tbody>
</table>
  </div>
</div>
</template>
<script>
import Comment from "../components/Comment.vue"
import axios from 'axios'
export default {
  name:'ThreadPage',
  data() {
    return {
      threads:[]
    }
  },
  methods: {
    fetchThreadsByUser(){
        axios
        .get("http://localhost:3000/threads/byuser",{
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
    clickThreadDetailfromThreadPage(thread){
      console.log('jalan');
      console.log(thread);
      this.$emit("threadDetailIdThread",'threadsDetail',thread)
    }
  },
  created() {
    this.fetchThreadsByUser()
  },
  components:{
    Comment
  }
}
</script>