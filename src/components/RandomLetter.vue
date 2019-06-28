<template>
    <div class="random-letter">
        <div class="letter">
            <span v-if="!countdown.active">{{ currentLetter }}</span>
            <span v-else>{{ countdown.count }}</span>
        </div>
        <div v-if="letterPool.length > 0 && !countdown.active" class="button big" @click="pickLetter">Pick letter</div>
        <div v-else class="button big disabled" @click="pickLetter">Pick letter</div>
        <br>
        <div class="button secondary" @click="newGame">Restart</div>

        <div class="used-letters">
            <div class="used-letter" v-for="letter in usedLetters" :key="letter" @click="returnToPool(letter)">{{letter}}</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            letterPool: localStorage.letterPool
                ? JSON.parse(localStorage.letterPool)
                : this.alphabeth(),

            currentLetter: localStorage.currentLetter || "-",

            // TODO: Put the logic of the countdown in a module
            countdown: {
                count: 0,
                active: false,
                start(callback) {
                    this.count = 5;
                    this.active = true;
                    const interval = setInterval(() => {
                        this.count -= 1;
                        if (this.count == 0) {
                            this.active = false;
                            callback();
                            clearInterval(interval);
                        }
                    }, 1000);
                }
            }
        };
    },
    methods: {
        pickLetter() {
            const pick = this.letterPool[
                Math.floor(Math.random() * this.letterPool.length)
            ];
            this.countdown.start(() => {
                this.letterPool = this.letterPool.filter(
                    letter => letter != pick
                );
                this.writeLocalStorage();
                this.currentLetter = pick.toUpperCase();
            });
        },
        alphabeth() {
            return "abcdefghijklmnopqrstuvwxyz".split("");
        },
        newGame() {
            this.letterPool = this.alphabeth();
            this.currentLetter = "-";
            this.writeLocalStorage();
        },
        writeLocalStorage() {
            localStorage.letterPool = JSON.stringify(this.letterPool);
            localStorage.currentLetter = this.currentLetter;
        },
        returnToPool(letter) {
            this.letterPool.push(letter)
            this.writeLocalStorage()
        }
    },
    computed: {
        usedLetters() {
            return this.alphabeth().filter(
                letter => !this.letterPool.includes(letter)
            );
        }
    }
};
</script>

<style>
.letter {
    font-size: 1700%;
    font-weight: bold;
}

.button {
    background: #2ecc71;
    color: #fff;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 8px;
    display: inline-block;
    margin: 5px;
    font-weight: bold;
}

.button.disabled {
    background: #bdc3c7;
    opacity: 0.5;
    pointer-events: none;
}

.button.big {
    font-size: 200%;
}

.button.secondary {
    background: #95a5a6;
}

.used-letters {
    margin: 20px;
    overflow-wrap: break-word;
    line-height: 40px;
}
.used-letter {
    background: #34495e;
    color: #fff;
    padding: 4px 8px;
    margin: 5px;
    border-radius: 3px;
    display: inline;
    text-transform: uppercase;
    cursor: pointer;
}

@media only screen and (min-device-width: 900px) {
    .used-letters {
        line-height: 70px;
    }
    .used-letter {
        font-size: 200%;
        padding: 10px 20px;
        border-radius: 8px;
    }
}
@media only screen and (max-device-height: 900px) {
    .letter {
        font-size: 1300%;
    }
}

@media only screen and (max-device-height: 600px) {
    .letter {
        font-size: 1000%;
    }
    .button.big {
        font-size: 150%;
    }
}
</style>
