<template>
  <div>
     <table class="table table-hover">
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
      
      >
      <th scope="row"
      @click="clickThreadDetail(thread)"
      >
        {{thread.title}}
        </th>
      <td>{{thread.description}}</td>
      <td>{{thread.Comments.length}}</td>

      <td><i class="fas fa-trash btn" @click.prevent="deleteThread(thread.id)" ></i></td>
  
      <td><i class="fas fa-edit btn" @click.prevent="editThread(thread.id)" ></i></td>
    </tr>
  </tbody>
</table>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name:'ThreadsThreadPage',
  data() {
    return {
      threads:[]
    }
  },
  methods: {
    fetchThreadsByUser(){
      axios
      .get("https://gym-freaks-new.herokuapp.com/threads/byuser",{
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
        this.$emit("threadDetailIdThreadPage",'threadsDetail',thread)
    },
    deleteThread(id){
        axios
        .delete(`https://gym-freaks-new.herokuapp.com/threads/${id}`,{
          headers:{
            access_token: localStorage.access_token
          }
        })
        .then(res=>{
        this.$emit("afterDelete",'homePage')
          swal({
          title: "SUCCESS",
          text: "thread success to delete",
          icon: "success",
          });
        })
        .catch(err=>{
          console.log(err);
          swal({
              title: "FAILED",
              icon: "error",
            });
        })
    },
    editThread(id){

    }
  },
  created() {
    this.fetchThreadsByUser()
  },
}
</script>