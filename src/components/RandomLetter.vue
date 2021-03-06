<template>
    <div class="random-letter">
        <div class="letter">
            <span v-if="!countdown.active">{{ currentLetter }}</span>
            <span v-else>{{ countdown.count }}</span>
        </div>
        <div
            v-if="letterPool.length > 0 && !countdown.active"
            class="button big"
            @click="pickLetter"
        >
            Random letter
            <i class="fas fa-dice"></i>
        </div>
        <div v-else class="button big disabled" @click="pickLetter">
            Random letter
            <i class="fas fa-dice"></i>
        </div>
        <br>
        <div v-if="!countdown.active" class="button secondary" @click="restartOpen = !restartOpen">
            Restart
            <i class="fa fa-sync-alt"></i>
        </div>
        <div v-else class="button secondary disabled">
            Restart
            <i class="fa fa-sync-alt"></i>
        </div>

        <div v-show="restartOpen">
            <span class="danger-text">Are you sure you want to restart?</span><br>
            <div class="button small danger" @click="newGame">Yes, restart</div>
            <div class="button small secondary" @click="restartOpen = !restartOpen">Cancel</div>
        </div>

        <div class="used-letters">
            <div v-if="usedLetters.length === 0" class="placeholder">
                <div class="used-letter"></div>
                <div class="small">Used letters will be displayed here</div>
            </div>
            <div
                class="used-letter"
                v-for="letter in usedLetters"
                :key="letter"
                @click="returnToPool(letter)"
            >{{letter}}</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            letterPool: localStorage.letterPool
                ? JSON.parse(localStorage.letterPool)
                : this.alphabet(),

            currentLetter: localStorage.currentLetter || "?",
            restartOpen: false,
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
                this.currentLetter = pick.toUpperCase();
                this.writeLocalStorage();
            });
        },
        alphabet() {
            return "abcdefghijklmnopqrstuvwxyz".split("");
        },
        newGame() {
            this.restartOpen = false;
            this.letterPool = this.alphabet();
            this.currentLetter = "?";
            this.writeLocalStorage();
        },
        writeLocalStorage() {
            localStorage.letterPool = JSON.stringify(this.letterPool);
            localStorage.currentLetter = this.currentLetter;
        },
        returnToPool(letter) {
            this.letterPool.push(letter);
            this.writeLocalStorage();
        }
    },
    computed: {
        usedLetters() {
            return this.alphabet().filter(
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

.danger-text {
    color: #e74c3c;
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

.button.danger {
    background: #e74c3c;
}

.button.disabled {
    background: #bdc3c7;
    opacity: 0.5;
    pointer-events: none;
}

.button.big {
    font-size: 200%;
}

.button.small {
    font-size: 80%;
    padding: 4px 10px;
    margin: 2px;
    color: #fff;
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

.placeholder .used-letter:before {
    content: "?";
}
.placeholder .used-letter {
    background: transparent;
    border: dashed 3px #ccc;
    color: transparent;
}

.small {
    color: #999;
    font-size: 0.9em;
    line-height: normal;
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
