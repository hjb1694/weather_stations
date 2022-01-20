<template> 
    <div v-if="isLoading" class="loading">Loading...</div>
    <div v-else-if="!isLoading && !isLoadError">
        <div class="stations-grid">
            <app-station 
            v-for="station of inViewStations" 
            :key="station.id"
            :station-name="station.properties.name"
            :station-id="station.properties.id"
            :latitude="station.geometry.coordinates[0]"
            :longitude="station.geometry.coordinates[1]"
            :elevation="station.properties.elevation.value"
            />
        </div>
        <button 
        @click="goToPrevious" 
        class="previous-btn"
        :disabled="previousBtnIsDisabled"
        >
        Previous
        </button>
        <button 
        @click="goToNext" 
        class="next-btn"
        :disabled="nextBtnIsDisabled"
        >
        Next
        </button>
    </div>
    <div class="error-msg" v-else>Oh No! An Error has Occurred!</div>
    
</template>

<script>
import Station from './station.component.vue';
export default {
    components: {
        'app-station': Station
    },
    data(){
        return {
            isLoadError: false,
            offset: 0, 
            inViewStations: [],
            allStations: [], 
            isLoading: false, 
            nextBtnIsDisabled: false, 
            previousBtnIsDisabled: true
        }
    },
    methods: {
        goToNext(){
            this.offset += 9;
            this.inViewStations = this.allStations.slice(this.offset, this.offset + 9);
            this.previousBtnIsDisabled = false;
            if(this.inViewStations.length < 9){
                this.nextBtnIsDisabled = true;
            }
        }, 
        goToPrevious(){
            this.offset -= 9;
            this.inViewStations = this.allStations.slice(this.offset, this.offset + 9)
            this.nextBtnIsDisabled = false;
            if(this.offset === 0){
                this.previousBtnIsDisabled = true;
            }
        }
    },
    created(){
        fetch('https://api.weather.gov/radar/stations')
        .then(resp => {
            if(!resp.ok){
                throw new Error('Fetch Failed');
            }

            return resp.json();
        })
        .then(data => {
            this.allStations = data.features;
            this.inViewStations = data.features.slice(this.offset, 9);
        })
        .catch(e => {
            console.error(e);
        });
    }
}
</script>

<style scoped>
    .stations-grid{
        display:grid;
        grid-template-columns:repeat(auto-fill, 20rem);
        grid-auto-rows:30rem;
        grid-gap:2rem;
        margin-top:3rem;
    }

    .next-btn, 
    .previous-btn {
        background:rgba(255,255,255,.3);
        backdrop-filter: blur(10px);
        font-size:2.5rem;
        border:none;
        display:inline-block;
        margin-top:3rem;
        padding:1rem;
        box-shadow: 0 0 .5rem rgba(0,0,0,.24);
        transition: transform .3s;
        margin-right:1rem;
    }

    .next-btn:hover{
        transform:scale(1.05);
    }

    .loading{
        font-size:2.5rem;
        color:#fff;
    }

    .error-msg{
        font-size:2rem;
        margin-top:3rem;
    }
</style>