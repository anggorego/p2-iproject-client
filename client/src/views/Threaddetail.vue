<template>
  <div class="row">
    <h3><span>title: </span>{{threadDetailId.title}}</h3>
    <p><span>desc: </span>{{threadDetailId.description}}</p>
    <p><span>by: {{threadDetailId.User.name}}</span></p>
    <p><span>comments: </span>{{threadDetailId.Comments.length}}</p>
<table class="table table-hover w-auto ">
  <thead>
    <tr>
      <th scope="col">name</th>
      <th scope="col">comment</th>
    </tr>
  </thead>
  <tbody>
    <tr class="table-dark"
       v-for="comment in comments"
      :key="comment.id"
      >
      <th scope="row">
        {{comment.User.name}}
        </th>
      <td>{{comment.description}}</td>
      <td><i class="fas fa-trash btn" @click.prevent="deleteComment(threadDetailId.id,comment.id)" ></i></td>
    </tr>
  </tbody>
</table>
  <Comment
  :threadData= "threadDetailId"
  @backToHome="backToHome"
  ></Comment>
  </div>
</template>
<script>
import Comment from "../components/Comment.vue"
import axios from 'axios'
export default {
  props:['threadDetailId'],
  name:'ThreadDetail',

  data() {
    return {
      comments:[]
    }
  },
  methods: {
    fetchThreadById(){
      axios
      .get(`https://gym-freaks-new.herokuapp.com/threads/${this.threadDetailId.id}`,{
         headers:{
            access_token: localStorage.access_token
          }
      })
      .then(res=>{
        
        this.comments = res.data.Comments
      })
      .catch(err=>{
        console.log(err);
      })
    },
    backToHome(page){
      this.$emit("backToHome",page)
    },
    deleteComment(threadid,commentid){
      
      axios
      .delete(`https://gym-freaks-new.herokuapp.com/comments/${threadid}/${commentid}`,{
        headers:{
          access_token: localStorage.access_token
        }
      })
      .then(res=>{
        this.$emit("afterDelete",'threadsPage')
            swal({
          title: "SUCCESS",
          text: "comment success to delete",
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
    }

  },
  created() {
    this.fetchThreadById()
  },
  components:{
    Comment,
  },
  watch:{
    "comments": function(val){
      // this.fetchThreadById()
    }
  }
}
</script>
<style scoped>
.row {
    display: -ms-flexbox;
    display: flex;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
    flex-direction: column;
    align-content: center;
    align-items: center;
}
</style>