<template>
    <div class="collection">
        <div v-for="(Cat, index) in storedCats" class="cat" @click="deleteCat(index)">
            <div class="container">
                <img :src="Cat.url" :alt="Cat.source_url">
            </div>
                
                <h5 class="text">{{ Cat.artist }}</h5>
            
            
        </div>
    </div>
</template>

<script>
export default {
    props:{
        stored:Array
    },
    computed: {
        storedCats() {
            return JSON.parse(JSON.stringify(this.stored));
        }
    },
    methods:{
        deleteCat(index){
            this.stored.splice(index,1);
            localStorage.setItem('CatBoys', JSON.stringify(this.stored));
        }
    }

}

</script>
<style>
    .collection{
        display: grid;
        grid-template-columns: repeat( auto-fill, minmax(220px, 1fr) );
        grid-template-rows: repeat( auto-fill, minmax(250px, 1fr) );
        gap:10px;
        
    }

    .container{
    width: 200px;
    height: 200px;
    transition: 0.3s ease-in;
    position: relative;
    cursor: pointer;
    }
    .container::before {
        content:"X";
        font-size: 148px;
        position: absolute;
        transform: translate(-50%, -50%);
        top: 50%;
        left: 50%;
        opacity: 0;
        z-index: 99;
        transition: 0.3s ease-in;
        cursor: pointer;
    }
    .container:hover img{
        opacity:0.5;
    }
    .container:hover:before {
        opacity: 1;
    }
    img:hover {
        transition: 0.5s ease-in;
    }
    img::before{
        content:"";
        width: 0;
        height:0;
        background-color: rgba(73, 73, 73, 0.279);
    }
    img:hover img::before {
        width: 100%;
        height:100%;
    }
    .cat {
        border: 2px solid black;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

</style>