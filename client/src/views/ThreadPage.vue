<template>
<div class="mt-5">
  <div>
  <ThreadsThreadPage
  @threadDetailIdThreadPage="threadDetailIdThreadPage"
  @afterDelete="afterDelete"
  ></ThreadsThreadPage>
  </div>
</div>
</template>
<script>
import Comment from "../components/Comment.vue"
import ThreadsThreadPage from "../components/threadsThreadPage.vue"
// import axios from 'axios'
export default {
  name:'ThreadPage',
  data() {
    return {
      threads:[]
    }
  },
  methods: {

    threadDetailIdThreadPage(page,thread){
  
      this.$emit('threadDetailId',page,thread)
    },
    afterDelete(page){
      this.$emit('afterDelete',page,thread)
    }
  },
  created() {
    // this.fetchThreadsByUser()
  },
  components:{
    Comment,
    ThreadsThreadPage
  }
}
</script>