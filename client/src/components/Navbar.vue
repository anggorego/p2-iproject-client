<template>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">GYM-FREAKS!</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="row collapse navbar-collapse" id="navbarColor01">
          <div>
            <ul class="navbar-nav me-auto">
              <li class="nav-item">
                <a class="nav-link active"
                href="#"
                @click.prevent="clickHrefHome"
                >Home
                </a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#"
                @click.prevent="clickHrefThread"
                >My Threads</a>
              </li>
                <li class="nav-item">
                <a class="nav-link" href="#"
                @click.prevent="clickHrefPost"
                >Post A Thread</a>
              </li>
            </ul>
          </div>
          <div>
            <ul class="navbar-nav me-auto">
              <li class="nav-item"><a class="nav-link" href="#"
              @click.prevent="clickHrefLogOut"
              >sign out</a></li>
              <li class="nav-item">
                <a class="nav-link">welcome: {{userName}}</a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </nav>
</template>
<script>
export default {
  name:'Navbar',
  props:['userName'],
  data() {
    return {
      
    }
  },
  methods: {
    clickHrefThread(){
      
      this.$emit("directToThreadsList","threadsPage")
    },
    clickHrefHome(){
      this.$emit("backToHome","homePage")
    },
    clickHrefLogOut(){
      this.$emit("backToLogin","loginPage")
    },
    clickHrefPost(){
      this.$emit("directToPostThread","threadForm")
    }

  },
}
</script>