<template>
  <div id="main">
    <button @click="fetchData">Fetch Another Image</button>
      <div v-if="(imgs && loading)" class="card">
        <img :src="imgs.url" :alt="imgs.source_url">
        <h1>{{imgs.artist}}</h1>
      </div>
      <div v-else>
        <h1>Loading...</h1>
      </div>
  </div>
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
  height: 800px;
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
margin: 50px 0;
width: fit-content;
cursor: pointer;
}
</style>
<script>
export default {
  data() {
    return {
      imgs:null,
      loading:false
    }
    
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
    
  }
},
mounted() {
this.fetchData()
}
}

</script>