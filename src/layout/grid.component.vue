<template>
    <div class="two-column">
        <div class="one">
            <slot name="side-panel">One</slot>
        </div>
        <div class="two">
            <slot name="main-area">Two</slot>
        </div>
    </div>
</template>

<style scoped>
    .two-column{
        display: grid;
        grid-template-columns:25% auto;
        height:100vh;
    }

    .one{
        background:rgba(255,255,255,.3);
        backdrop-filter: blur(10px);
        box-shadow:0 0 .5rem rgba(0,0,0,.4);
    }

    .two{
        padding:2rem;
        overflow-y:auto;
    }
</style>