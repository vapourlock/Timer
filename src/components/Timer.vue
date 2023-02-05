<template>
    <div class="box">
        <h1>{{ timerCount }} seconds left</h1>
        <input v-model="seconds"/>seconds<br />
        <input v-model="minutes"/>minutes<br />
        <button v-on:click="startTimer">Start</button>
        <button v-on:click="resetTimer">Reset</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                timerCount: null,
                seconds: null,
                minutes: null,
            }
        },
        watch: {
            timerCount: {
                handler(value) {
                    if (value > 0) {
                        setTimeout(() => {
                            this.timerCount--;
                        }, 1000);
                    }else if( this.seconds || this.minutes)
                    {
                        this.playBuzzer();
                    }
                },
            }
        },
        methods: {
            async startTimer() {
                this.timerCount = this.seconds || this.minutes * 60;
            },
            async resetTimer() {
                this.timerCount = null;
                this.seconds = null;
                this.minutes = null;
            },
            async playBuzzer() {
                const path = '/assets/audio/buzzer.wav'
                const audio = new Audio(path);
                audio.play();
            }
        }
    }
</script>

<style scoped>
.box {
    border-style: solid;
    padding: 1em;
}
</style>