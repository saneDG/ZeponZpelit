<template>
    <div id='app'>
        <img class='background' src='img/zeppo.png' alt='zeppo' />
        <Game></Game>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import Game from "./views/Game.vue";


export default Vue.extend({
    name: "App",
    components: {
        Game,
    },
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");
#app {
    font-family: "VT323", monospace;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #bdff51;
}
html {
    margin: 0;
    padding: 0;
    background-color: #930000;
}
body {
    margin: 0;
    padding: 0;
}
.background {
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
}
</style>
