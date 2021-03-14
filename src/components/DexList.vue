<template>
    <div class="dex-list row">
        <DexCard v-for="pokemon in list" :key="pokemon.id" :pokemon="pokemon"/>
        <!-- <div v-for="pokemon in list" :key="pokemon.id">{{pokemon}}</div> -->
    </div>
</template>

<script>
import DexCard from './DexCard'; 

export default {
    props: {
        list: {
            type: Array,
            required: true
        }
    },
    components: {
        DexCard
    }
}
</script>

<style scoped>

.dex-list {
    margin-bottom: 5rem;
}
</style>
