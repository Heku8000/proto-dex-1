<template>
    
    <section class="dex-card">
        <div class="dex-card__side dex-card__side--front">
            <h4 class="dex-card__heading text-center">
                <img v-bind:src="official_artwork.url" alt="" class="dex-card__heading-image">
            </h4>
            <div class="dex-card__details">
             
            </div>
            <div class="dex-card__footer">
                <span class="dex-card__footer-pkmDexName">
                    <div class="dex-card__footer-pkmDexName-dexnum">
                        #{{pokemon.id}} 
                    </div>
                    <div class="dex-card__footer-pkmDexName-name">
                        {{pokemon.species.name}}
                    </div>
                </span>
            </div>
        </div>

        <div class="dex-card__side dex-card__side--back">         
            <div class="dex-card__pkmnDetails">
                <div class="side--back__img">
                    <div class="dex-card__pkmnDetails-img">
                    <img v-bind:src="pokemon.sprites.front_default" alt="">
                    </div>
                    <div class="dex-card__pkmnTypes">
                        <span class="pkmnType" v-for="type in pokemon.types" :key="type.name"> {{type.type.name}} </span>
                    </div>
                </div>    
                <div class="dex-card__pkmnDetails-dimensions row justify-content-center mt-2">
                    <span class="col-md-6 col-sm-12 text-right text-sm-center text-xs-center dex-card__weight"><img class="icon-weight" src="../assets/weight.svg" alt=""> {{format_weight}} kg  </span>
                    <span class="col-md-6 col-sm-12 text-left text-sm-center text-xs-center dex-card__height"><img class="icon-height" src="../assets/height.svg" alt=""> {{format_height}} m</span>       
                </div>
                <div class="dex-card__pkmnDetails-attrs row justify-content-center align-items-center">
                    <div class="ability-title text-center">Habilidades</div>
                    <div class="col-md-12 text-center pkmnDetails-ability" v-for="ability in pokemon.abilities" :key="ability.name">{{ability.ability.name}}</div>
                </div>
                
            </div>
        
        </div>
    </section>
</template>

<script>

export default {
    props: {
        pokemon: {
            type: Object,
            required: true,
        },
    },
    data() {
        let format_weight = this.pokemon.weight/10;
        let format_height = this.pokemon.height/10;
        return {
            official_artwork: {
                url: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+this.pokemon.id+".png"
            },
            format_weight,
            format_height
        }        
    }    
}

</script>

<style scoped>

    .dex-card {
        height: 45vh;
        width: 22%;
        margin: 1rem;
        padding: 2rem;
        perspective: 150rem;
        -moz-perspective: 150rem;
        -webkit-perspective: 150rem;
        position: relative;
    }

    .dex-card__heading-image {
        width: 80%;
        overflow: hidden;
    }

    .dex-card__side {
        font-size: 1.5rem;
        transition: all .8s ease;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        position: absolute;
        top: 0;
        left: 0;
        border-radius: 3px;
        overflow: hidden;
        border: 2px solid black;
        box-shadow: 1px 1px 2px black;
    }

    .dex-card__side--back{
        background-image: linear-gradient(to bottom, rgba(255, 255, 255, 0.692), rgba(240, 240, 240, 0.6)),
        url(../assets/pkball_icon.png);
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
        transform: rotateX(180deg);
    }

    .dex-card:hover .dex-card__side--front{
        transform: rotateX(-180deg);
    } 

    .dex-card:hover .dex-card__side--back {
        transform: rotateX(0);
    }

    .dex-card__footer{
        padding-bottom: 1rem;
        border-top: 2px solid black;
    }

    .dex-card__footer-pkmDexName-dexnum{
        display: inline-block;
        padding: .5rem 2rem .5rem .5rem;
        background-color: rgb(255, 0, 0);
        color: white;
        font-weight: 700;
        clip-path: polygon(0% 0%, 76% 0, 100% 0%, 75% 100%, 0% 100%);
    }

    .dex-card__footer-pkmDexName-name {
        display: inline-block;
        text-transform: capitalize;
        font-weight: 700;
    }

    .dex-card__pkmnTypes {
        display: inline-block;
        text-transform: capitalize;
        padding-left: 1.5rem;
        font-size: 1.2rem;
        font-weight: 700;
    }

    .pkmnType {
        margin-top: .8rem;
    }
    
    .side--back__img {
        border-bottom: 1px solid black;
    }

    .dex-card__pkmnDetails-img {
        display: inline-block;
    }

    .dex-card__pkmnDetails-attrs {
        width: inherit !important;
        display: block;
        text-transform: capitalize;
    }

    .dex-card__pkmnDetails-dimensions {
        padding: 1rem 0 1.5rem 0;
    }

    .dex-card__abilities {
        width: 100%;
        background-color: orangered;
        list-style: none;
    }

    .dex-card__weight {
        font-size: 1.2rem;
    }

    .dex-card__height {
        font-size: 1.2rem;
    }

    .icon-weight {
        width: 1.5rem;
        margin-bottom: .5rem;
    }

    .icon-height {
        width: 1.5rem;
    }

    .pkmnAttr {
        font-size: 1.2rem;
        margin-right: 2rem;
        margin-left: -1.4rem;
    }

    .ability-title {
        background: rgba(240, 240, 240, 0.6);
        border-top: 1px solid black;
        border-bottom: 1px solid black;
        font-weight: 700;
    }

    .pkmnDetails-ability {
        font-size: 1.2;
    }

    @media(max-width: 760px) {
        
        .dex-card {
            height: 60vh;
            width: 100%;
        }

        .dex-card__heading-image {
            width: 70%;
            overflow: hidden;
        }
    }





</style>