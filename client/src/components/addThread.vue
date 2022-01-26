<template>
  <div class="">
    <form>
    <legend>Post A thread</legend>
    <div class="form-group">
      <label for="exampleInputPassword1" class="form-label mt-4">Title</label>
      <input type="password" class="form-control" id="exampleInputPassword1" placeholder="full name">
      <label for="exampleTextarea" class="form-label mt-4">description</label>
      <textarea class="form-control" id="exampleTextarea" rows="3"></textarea>
    </div>
    <button type="submit" class="btn btn-secondary">Submit</button>
</form>
  </div>
</template>
<script>
export default {
  name:'AddThread',
  data() {
    return {
      
    }
  },
}
</script>