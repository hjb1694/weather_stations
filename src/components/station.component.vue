<template> 
    <div class="tile">
        <h2 class="station-name">{{ stationName }}</h2>
        <h3 class="station-id">{{ stationId }}</h3>
        <div class="coords"> 
            <p>
                <strong>Lat:</strong> {{ latitude }}
            </p>
            <p>
                <strong>Lon:</strong> {{ longitude }}
            </p>
        </div>
        <div class="elevation">
           <strong>Elevation:</strong> {{ elevation }}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        stationName: {
            type: String, 
            required: true
        }, 
        stationId: {
            type: String, 
            required: true
        }, 
        latitude: {
            type: Number, 
            required: true
        }, 
        longitude: {
            type: Number, 
            required: true
        }, 
        elevation: {
            type: Number, 
            required: true
        }
    }
}
</script>

<style scoped>
    .tile{
        background:rgba(255,255,255,.3);
        backdrop-filter: blur(10px);
        box-shadow:0 0 .5rem rgba(0,0,0,.24);
        padding:1.5rem;
    }

    .station-name{
        font-size:2rem;
    }

    .coords{
        margin:2rem 0;
        font-size:1.8rem;
    }

    .elevation{
        font-size:1.6rem;
    }
</style>