<template>
    <div class='buttons'>
        <button
            v-for='btn in buttonData'
            :class='(nextButton === btn.id && lastClickedButton !== btn.id) ? btn.name : ""'
            :key='btn.id'
            @click='isTheRightButton(btn.id), lastClickedButton = btn.id'></button>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "Buttons",
    props: {
        state: {
            required: true,
            type: String,
        },
    },
    data() {
        return {
            buttonData: [
                { id: 0, name: "blue", color: "#0085E5" },
                { id: 1, name: "yellow", color: "#E5D200" },
                { id: 2, name: "green", color: "#26E500" },
                { id: 3, name: "red", color: "#E50000" },
            ] as any,
            history: [] as any,
            prevButton: null as any,
            nextButton: null as any,
            lastClickedButton: null as any,
            interval: 1000,
            delta: 40,
            breakpoint: 1,
            score: 0,
            counter: 0,
            level: 0,
        };
    },
    watch: {
        state(value: string) {
            console.log("gamestarted");
            console.log(value);
            if (value === "PLAYING") {
                this.timer();
            } else if (value === "GAMEOVER") {
                this.interval = 0;
            }
        },
    },
    mounted() {
        console.log(this.buttonData);
        // this.timer();
    },
    methods: {
        timer() {
            console.log(this.interval);
            console.log(this.state);

            // nullitetaan viimaksi klikattu nappi että nappi voi taas palaa.
            // jokaiselle napille tehty :class tarkastus tämän muuttujan perusteella.
            this.lastClickedButton = null;

            this.prevButton = this.nextButton;
            this.nextButton = this.generateRandom(this.prevButton);
            this.history.push(this.nextButton);

            this.nextInterval();

            if (this.interval >= 40) {
                setTimeout(this.timer, this.interval);
            }
        },

        isTheRightButton(buttonID: number) {
            if (buttonID === this.history[0]) {
                this.history.shift();
                this.score++;
                this.$emit("new-score", this.score);
                console.log("right");
            } else {
                this.$emit("game-over", this.score);
                this.state = "GAMEOVER";
                console.log("game over");
                console.log(
                    "FINAL SCORE:::::::::_____----<>>><<<<<->>>>>",
                    this.score,
                    "<<<<<<<<<<<<<<<<<<<<<------------"
                );
                this.interval = 0;
            }
        },

        nextInterval() {
            const breakpoint = this.breakpoint;
            this.counter++;
            console.log("COUNTING", this.counter);

            if (this.counter > breakpoint) {
                this.level++;
                this.counter = 0;
                this.interval -= this.delta - this.level;
                this.breakpoint++;
                console.log(this.interval);
            }
        },

        generateRandom(same: number): number {
            const num = Math.floor(Math.random() * 4);
            // prevent same as last
            return num === same ? this.generateRandom(same) : num;
        },
    },
});
</script>

<style lang="scss">
.buttons {
    position: relative;
    margin-top: 60vh;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    button {
        display: block;
        width: 230px;
        height: 230px;
        border-radius: 50%;
        background-color: rgb(185, 185, 185);
    }
    .blue {
        background-color: #0085e5;
    }
    .yellow {
        background-color: #e5d200;
    }
    .green {
        background-color: #26e500;
    }
    .red {
        background-color: #e50000;
    }
}
input[type="button"] {
    outline: none;
}
input[type="button"]::-moz-focus-inner {
    border: 0;
}
button:focus {
    outline: 0 !important;
}
button:active {
    transform: scale(0.96)
}
</style>
