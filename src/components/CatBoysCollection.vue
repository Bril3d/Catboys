<template>
    <div class="collection">
    <div v-for="Cat in storedCats" class="container">
       
            <img :src="Cat.url" :alt="Cat.source_url">
            <h5>{{ Cat.artist }}</h5>
        
        
    </div>
    </div>
</template>
<style scoped>
    .collection{
        display: grid;
        grid-template-columns: repeat( auto-fill, minmax(200px, 1fr) );
        grid-template-rows: repeat( auto-fill, minmax(250px, 1fr) );
        gap:10px;
    }
    .container{
    width: 200px;
    height: 200px;
    color: red;
    text-align: center;
    }

</style>
<script>
export default {
    props:{
        stored:Array
    },
    computed: {
        storedCats() {
            return JSON.parse(JSON.stringify(this.stored));
        }
    }

}

</script>