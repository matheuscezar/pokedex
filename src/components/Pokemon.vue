<template>
  <div>
    <div class="card" id="pokeCard">
      <div class="card-image">
        <figure>
          <img :src="pokemon.front">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{name | upper}}</p>
            <p class="subtitle is-6">{{pokemon.type}}</p>
          </div>
        </div>
        <div class="content">

        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';
export default {
  created: function() {
    axios.get(this.url).then(res =>{
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
    })
  },
  data(){
      return {
        pokemon: {
          type:'',
          front:'',
          back:''
        }
      }
    },
  props:{
    name:String,
    url: String
  },
  filters:{
    upper: function (value){
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

<style scoped>
  #pokeCard{
    margin-top: 10px;

  }
  #pokeCard:hover{
    background-color: aqua;
  }
</style>