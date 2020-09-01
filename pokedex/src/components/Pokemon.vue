<template>
    <div id="pokemon">

    <div class="card " style="width: 18rem;">
    
        <div>
            <figure>
            <img class="card-img-top" :src="currentImg" alt="Placeholder image">
            </figure>
        </div>

        <div class="card-body" >
            <p class="title font-weight-bold">{{num}} {{name | upper}}</p>
            <p class="subtitle">{{pokemon.type}}</p>
        </div>

        <div>
           <button type="button" class="btn btn-outline-dark mb-3" @click="mudarSprite">Mudar Sprite</button>
        </div>
    </div>


    </div>
  
      
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res => {
                this.pokemon.type = res.data.types[0].type.name;
                this.pokemon.front = res.data.sprites.front_default;
                this.pokemon.back = res.data.sprites.back_default;
                this.currentImg =  this.pokemon.front;
                console.log(this.pokemon);
        })
    },
    data(){
        return{
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }
            else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}


</script>


<style>
#pokemon{
    margin-top: 2%;
}
</style>
