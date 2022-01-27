<template>
  <div class="row mt-5">
    <div class="card">
      <form>
          <h2>BMR CALCULATOR</h2>
          <h5>Basal Metabolic Rate</h5>
          <h2
          v-if="foodValue"
          >result:{{bmrResult.bmr}} </h2>
          <div class="flex form-group">
            <label class="col-form-label col-form-label-sm mt-4" for="inputSmall">WEIGHT (.Kg)</label>
            <input class="form-control form-control-sm" type="text"  id="inputSmall"
            v-model="weight"
            >
              <label class="col-form-label col-form-label-sm mt-4" for="inputSmall">HEIGHT (.Cm)</label>
            <input class="form-control form-control-sm" type="text"  id="inputSmall"
            v-model="height"
            >
              <label class="col-form-label col-form-label-sm mt-4" for="inputSmall">AGE</label>
            <input class="form-control form-control-sm" type="text"  id="inputSmall"
            v-model="age"
            >
              <label class="col-form-label col-form-label-sm mt-4" for="inputSmall">SEX</label>
            <input class="form-control form-control-sm" type="text"  id="inputSmall"
            v-model="sex"
            >
          </div>
          <center><button type="submit" class="btn btn-primary mb-3"
          @click.prevent="bmwCalculatorApi"
          >Submit</button></center>
      </form>
    </div>
    <div>
    <small>click to post</small><br>
     <i class="fas fa-plus btn"
      @click="directToThreadsList"
     ></i>
      <Threads
      @threadDetailId="threadDetailId"
      ></Threads>
    </div>
    <div class="card">
      <form>
          <h2>Food Calories</h2>
           <small>type down here</small>
          <div class="form-group">
            <label class="col-form-label col-form-label-sm mt-4" for="inputSmall">Food Name</label>
            <input class="form-control form-control-sm" type="text"  id="inputSmall"
            v-model="food"
            >
  
          </div>
          <center><button type="submit" class="btn btn-primary mb-5"
          @click.prevent="foodCalculator"
          >Submit</button></center>
      </form>

    <div class="mr-3"
    v-if="foodResult.name.length > 0"
    >
      <small>{{foodResult.name}}</small>
      <table style="border: 1px solid">
        <thead style="border: 1px solid">
          <tr >
            <th style="border: 1px solid">Energi KCAL</th>
            <th>FAT</th>
          </tr>
        </thead>
        <tbody style="border: 1px solid">
          <tr>
            <td style="border: 1px solid">{{foodResult.nutrient["ENERC_KCAL"]}}</td>
            <td>{{foodResult.nutrient["FAT"]}}</td>
          </tr>
        </tbody>
      </table>
    </div>
    </div>
  </div>
</template>
<script>
import Navbar from "../components/Navbar.vue"
import AddThread from "../components/addThread.vue"
import Threads from "../components/threads.vue"
import axios from 'axios'


export default {
  name:'Home',
  data() {
    return {
      threads:[],
      thread:{},
      user:'',
      weight:'',
      height:'',
      age:'',
      sex:'',
      bmrResult:{},
      food:'',
      foodResult:{
        name:'',
        nutrient:{}
      },
      foodValue:false

    }
  },
  methods: {
    threadDetailId(page,thread){
      this.$emit('threadDetailId',page,thread)
    },
    clickHrefThread(){
      
      this.$emit("directToThreadsList","threadForm")
    },
    fetchUser(){
      axios
        .get("https://gym-freaks-new.herokuapp.com/user",{
          headers:{
            access_token: localStorage.access_token
          }
        })
        .then(res=>{
          this.user = res.data.name
          this.$emit("userData",this.user)
        })
        .catch(err=>{
          console.log(err);
        })
    },
    bmwCalculatorApi(){
      if(!this.sex ||!this.weight||!this.height||!this.age ){
        swal({
        title: "FAILED",
        text: "Please enter all datas",
        icon: "error",
      });
      }
    axios
      .get(`https://gym-freaks-new.herokuapp.com/bmr?weight=${this.weight}&&height=${this.height}&&age=${this.age}&&sex=${this.sex}`)
      .then(res=>{
        this.weight='',
        this.height='',
        this.age=''
        this.sex=''
            swal({
            title: "SUCCESS",
            text: `your BMR : ${res.data.bmr} `,
            icon: "success",
            });
        this.bmrResult = res.data
        this.foodValue = true
      })
      .catch(err=>{
          console.log(err);
        swal({
        title: "FAILED",
        icon: "error",
      });
      })
    },
    directToThreadsList(){
      
      this.$emit("directToThreadsList","threadForm")
    },
    foodCalculator(){

      if(!this.food){
                swal({
        title: "FAILED",
        text: "Please enter food name",
        icon: "error",
      });

      }
      axios
      .get(`https://api.edamam.com/api/food-database/v2/parser?app_id=a96fddc0&app_key=e6dcb91182b1a50c7431a62b17dd7f92&ingr=${this.food}`)
      .then(res=>{
      
        this.foodResult.nutrient = res.data.parsed[0].food.nutrients
        this.foodResult.name = res.data.parsed[0].food.label
      })
      .catch(err=>{
        console.log(err);
      })
    }
  },
  components:{
    Navbar,
    AddThread,
    Threads,
    // Loader
  },
  created() {
    
    this.fetchUser()
  },
}
</script>
<style scoped>
.row{
  justify-content: space-evenly;
  
}
.card{
  justify-content: space-around;
}
</style>