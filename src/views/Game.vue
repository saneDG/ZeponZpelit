<template>
    <div id='game'>
        <Score :score='score' :state='state' @start='startTheGame'>
        </Score>
        <Buttons
            @new-score='sendNewScore'
            @game-over='finalScore'
            :score='score'
            :state='state'>
        </Buttons>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import Buttons from "../components/Buttons.vue";
import Score from "../components/Score.vue";

export default Vue.extend({
    name: "App",
    components: {
        Buttons,
        Score,
    },
    data() {
        return {
            score: 0,
            state: "START",
        };
    },
    methods: {
        sendNewScore(value: number) {
            this.score = value;
        },
        finalScore(value: number) {
            this.score = value;
            this.state = "GAMEOVER";
        },
        startTheGame(state: string) {
            this.state = state;
            console.log("asdölasdökaslökdasökdöasdk", this.state);
            this.score = 0;
        }
    }
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
