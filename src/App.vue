<template>
  <div id="main">
    <div>
      <button @click="fetchData">Fetch Another Image</button>
      <button @click="saveCat">Save It</button>
    </div>

      <div v-if="(imgs && loading)">
        <div class="card">
          <img :src="imgs.url" :alt="imgs.source_url">
        </div>
        
        <h1 class="text">{{imgs.artist}}</h1>
      </div>
      
      <div v-else>
        <h1>Loading...</h1>
      </div>
      
  </div>
  <CatBoysCollection :stored="this.stored"></CatBoysCollection>
</template>
<style>
body {
background-color: aqua;
font-family: sans-serif;
}
#main {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
.card {
  width: 500px;
  height: 700px;
}
.text {
  color: red;
  text-align: center;
}
img {
  object-fit: cover;
  width: 100%;
  height: 100%;

}
button{
padding: 5px 10px;
border-radius: 5px;
background-color: white;
color: red;
margin: 50px 10px;
width: fit-content;
cursor: pointer;

}
</style>
<script>
import CatBoysCollection from "./components/CatBoysCollection.vue";
export default {
  data() {
    return {
      imgs:null,
      loading:false,
      stored:[],
    }
    
  },
  components:{
    CatBoysCollection
},
methods: {
  async fetchData(){
    this.loading = false;
    const res = await fetch('https://api.catboys.com/img');
    const json = await res.json();
    this.imgs = json;
    setTimeout(()=>{
      this.loading = true;
    },1000)
    
  },
  saveCat(){
    this.stored.push(this.imgs)
    localStorage.setItem('CatBoys', JSON.stringify(this.stored));
  }
},
mounted() {

if(localStorage.CatBoys){
  this.stored = JSON.parse(localStorage.getItem("CatBoys"));
};
this.fetchData()
}
}

</script>