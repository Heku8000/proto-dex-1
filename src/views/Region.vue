<template>
  <div class="home">
    <div class="row justify-content-center mb-3">
        <h1 class="col-md-12 text-center my-5">Ver Por Región</h1>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('kanto')">Kanto</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('johto')">Johto</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('hoenn')">Hoenn</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('sinnoh')">Sinnoh</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('unova')">Unova</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('kalos')">Kalos</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('alola')">Alola</button>
        <button class="btn btn-danger col-md-1" v-on:click="renderList('galar')">Galar</button>
    </div>
    <div class="row justify-content-center my-4">
        <div class="col-sm-3 col-xs-3 text-lg-right text-xs-center"><button v-on:click="previousPage" v-if="previousurl != null" class="btn btn-pag btn-previous" ><img src="../assets/left-arrow.svg" alt=""></button></div>
        <div class="col-sm-3 col-xs-3 text-lg-left text-xs-center"><button  v-on:click="nextPage" v-if="nexturl != null" class="btn btn-pag btn-next"><img src="../assets/left-arrow.svg" alt="" class="next-arrow"></button></div>
    </div>
    <DexList :list="pokemon"/>
  </div>
</template>

<script>
// @ is an alias to /src
//componentes
import DexList from '../components/DexList';
import axios from "axios";
//import data from "../assets/mock-up-pokemon.json";

export default {
  name: 'Home',
  components: {
    DexList
  },
  data() {
    return {
      //pokemon: this.data.pokemon,
      pokemon: [],
      testData: [],
      nexturl: null,
      previousurl: null
    }
  },
   mounted () {
    this.renderList("kanto");
  },
  methods: {  

    /**
     *  Esta es la función que llama al API de pokemon
     *  y procesa la información JSON dentro de un arreglo
     *  que se manda como prop al elemento de lista. También
     *  se aprovechan los pelementos de paginación que proporciona
     *  el API para generar la paginación de este módulo, guardando
     *  en data() los url para hacer las llamadas de paginacion 
     *  anterior y siguiente. 
     * 
     *  @param {String} region - el nombre de la region que será mostrada 
     */   

    renderList: function(region) {
        let offset = 0;

        switch (region){
        case "johto":
            offset = 151;
            break;
        case "hoenn":
            offset = 251;
            break;
        case "sinnoh":
            offset = 386;
            break;
        case "unova":
            offset = 495;
            break;
        case "kalos":
            offset = 649;
            break;
        case "alola":
            offset = 721;
            break;
        case "galar":
            offset = 810;
            break;
    }
   
    axios
      .get('https://pokeapi.co/api/v2/pokemon/?limit=24&offset='+offset)
      .then(response => {
            this.pokemon = [];
            if(response.data.next != null){
                this.nexturl = response.data.next;
            }else{
                this.nexturl = null;
            }
            if(response.data.previous != null){
                this.previousurl = response.data.previous;
            }else{
                this.previousurl = null;
            }
            
            response.data.results.forEach(element => {
                axios.get(element.url)
                .then(response => {
                    this.pokemon.push(response.data);
                });   
            });   
      });
    },
    
    nextPage: function() {
        axios.get(this.nexturl)
        .then(response => {
                this.pokemon = [];
                this.nexturl = response.data.next;
                if(response.data.previous != null){
                    this.previousurl = response.data.previous;
                }
                response.data.results.forEach(element => {
                    axios.get(element.url)
                    .then(response => {
                        this.pokemon.push(response.data);
                    });   
                });
        });
    },
    previousPage: function() {
        if(this.previousurl != null){
            axios.get(this.previousurl)
            .then(response => {
                    this.pokemon = [];
                    this.previousurl = response.data.previous;
                    if(response.data.next != null){
                    this.nexturl = response.data.next;
                    }
                    response.data.results.forEach(element => {
                        axios.get(element.url)
                        .then(response => {
                            this.pokemon.push(response.data);
                        });   
                    });
            });
        }else{
            console.log("No hay previo!");
        }
    }
  }
}
</script>


<style scoped>
    .btn-pag {
        width: 25%;
        padding: 0.5rem 1rem;
        background-color: rgb(163, 163, 163);
        border-radius: 30%;
        transition: all .3s;
    }

    .btn:hover {
        transform: translateX(3rem);
        transform:scale(1.1)
    }

    .btn-danger {
        margin: 0 1.3rem;
        background-color: rgb(245, 52, 52);
        font-weight: 600;
        transition: all .3s;
    }

    .next-arrow {
        transform: rotate(180deg)
    }

    @media (max-width: 575px){

        .btn-pag {
            width: 20%;
        }
    }
</style>