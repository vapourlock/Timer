<template>
    <div class="box" :class="{ active: started }">
        <h1 class="center">{{minutesLeftDisplay}}:{{secondsLeftDisplay}}</h1>
        <input v-model="seconds"/>seconds<br />
        <input v-model="minutes"/>minutes<br />
        <button v-on:click="startTimer">Start</button>
        <button v-on:click="resetTimer">Reset</button>
    </div>
</template>

<script>
    export default {
        props: {
            defaultSecStart: {
                type: Number,
                default: null
            },
            defaultMinStart: {
                type: Number,
                default: null
            },  
        },
        data() {
            return {
                timerCount: null,
                seconds: null,
                minutes: null,
                started: false,
                secondsLeftDisplay: 0,
                minutesLeftDisplay: 0,
            }
        },
        created(){
            this.seconds = this.defaultSecStart || null;
            this.minutes = this.defaultMinStart || null;
        },
        watch: {
            timerCount: {
                handler(value) {
                    if(this.started){
                        if (value > 0) {
                            setTimeout(() => {
                                this.timerCount--;
                                this.minutesLeftDisplay = Math.floor(this.timerCount/60);
                                this.secondsLeftDisplay = this.timerCount%60;
                            }, 1000);
                        }else if( this.seconds || this.minutes)
                        {
                            this.playBuzzer();
                        }
                    }
                },
            }
        },
        methods: {
            async startTimer() {
                this.started = true;
                this.timerCount = this.seconds || this.minutes * 60;
            },
            async resetTimer() {
                this.seconds = this.defaultSecStart;
                this.minutes = this.defaultMinStart;
                this.timerCount = null;                
            },
            async playBuzzer() {
                const path = '/assets/audio/buzzer.wav'
                const audio = new Audio(path);
                audio.play();
            },
        },
    }
</script>

<style scoped>
.box {
    border-style: solid;
    padding: 1em;
}
.center {
    text-align: center;
}

.active {
    background-color: rgb(131, 233, 131);
}
</style>