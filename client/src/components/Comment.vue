<template>
  <div class="row">
    <div class="form-group">
  <label for="exampleTextarea" class="form-label mt-4">comment below</label>
  <textarea class="form-control" id="exampleTextarea" rows="2" cols="100"
  v-model="descriptionComment"
  ></textarea>
  <button type="submit" class="btn btn-secondary"
  @click="clickButtonComment(threadData.id)"
  >Submit</button>
</div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props:['threadData'],
  name:'Comment',
  data() {
    return {
      descriptionComment:'',

    }
  },
  methods: {
    clickButtonComment(id){
      axios
      .post(`http://localhost:3000/comments/${id}`,{
        description: this.descriptionComment
      },{
         headers:{
            access_token: localStorage.access_token
          }
      })
      .then(res=>{
     
        this.$emit("backToHome",'homePage')
       
      })
      .catch(err=>{
        console.log(err);
      })
    },


  },
}
</script>