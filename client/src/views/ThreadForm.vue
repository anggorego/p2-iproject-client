<template>
    <div class="row mt-5">
    <form>
    <legend>Post A thread</legend>
    <div class="form-group">
      <label for="exampleInputPassword1" class="form-label mt-4">
      Title</label>
      <input type="text" class="form-control" id="exampleInputPassword1"
      v-model="titleForm"
      >
      <label for="exampleTextarea" class="form-label mt-4">description</label>
      <textarea class="form-control" id="exampleTextarea" rows="3"
      v-model="descForm"
      ></textarea>
    </div>
    <button type="submit" class="btn btn-secondary"
    @click.prevent="clickButtonThread"
    >Submit</button>
</form>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name:'ThreadForm',
  data() {
    return {
      titleForm:'',
      descForm:''
    }
  },
  methods: {
    clickButtonThread(){
      axios
      .post("http://localhost:3000/threads",{
        title:this.titleForm,
        description:this.descForm
      },{
        headers:{
            access_token: localStorage.access_token
          }
      })
      .then(res=>{
      
        this.$emit("afterPostThread","homePage")
      })
      .catch(err=>{
        console.log(err);
      })
    }
  },
}
</script>