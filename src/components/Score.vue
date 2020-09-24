<template>
    <div class='score'>
        <div class='container' @click='zeppoClicked(state)'>
            <h1 v-if='state === "PLAYING" || state === "GAMEOVER"'>{{ score }}</h1>
            <h1 v-else>{{ state }}</h1>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "Buttons",
    components: {},
    props: {
        state: {
            default: null,
            type: String,
        },
        score: {
            default: null,
            type: Number,
        },
    },
    data() {
        return {};
    },
    methods: {
        zeppoClicked(state: string) {
            if (state === "START") {
                console.log("steit on start");
                this.$emit("start", "PLAYING");
            } else {
                console.log("something else clicked");
            }
        },
    },
});
</script>

<style lang="scss">
.score {
    position: fixed;
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    top: 25vh;
    left: 20px;
    .container {
        background-color: #1d191a;
        height: 190px;
        min-width: 300px;
        display: flex;
        text-align: center;
        align-items: center;
        h1 {
            font-size: 144px;
            text-shadow: 0px 0px 8px #bdff51;
            margin: 0 auto;
        }
    }
}
</style>