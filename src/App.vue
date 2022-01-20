<template>
    <app-grid>
        <template #side-panel>

        </template>
        <template #main-area>
            <h1>Weather Stations</h1>
            <app-stations/>
        </template>
    </app-grid>
</template>

<script>
import Grid from './layout/grid.component.vue';
import Stations from './components/stations.component.vue';
export default {
    components: {
        'app-grid': Grid, 
        'app-stations': Stations
    }
}
</script>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:inherit;
}

html{
    box-sizing: border-box;
    font-size:62.5%;
    height:100%;
}

body{
    height:100%;
    background:url('./assets/sky.jpg') center / cover;
    font-family: 'Dosis', sans-serif;
}

h1{
    color:#fff;
    font-size:4rem;
    font-weight:600;
    text-shadow:2px 2px 2px #000;
}

button{
    cursor:pointer;
}
</style>