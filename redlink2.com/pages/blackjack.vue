<template>
<body>
    <div>
        <div class="container">
            <div class="opHand">
                <div class="oCard1" v-if="dealt">
                    <img :src="require(`~/assets/cards/${opHand[0]}.png`)" />
                </div>
                <div class="oCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="oCard2" v-if="dealt">
                    <img :src="require(`~/assets/cards/${opHand[1]}.png`)" />
                </div>
                <div class="oCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="oCard3" v-if="dealt">
                    <img :src="require(`~/assets/cards/${opHand[2]}.png`)" />
                </div>
                <div class="oCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="oCard4" v-if="dealt">
                    <img :src="require(`~/assets/cards/${opHand[3]}.png`)" />
                </div>
                <div class="oCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="oCard5" v-if="dealt">
                    <img :src="require(`~/assets/cards/${opHand[4]}.png`)" />
                </div>
                <div class="oCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
            </div>
            <div class="btns1">
                <button v-on:click="stay" class="btns">STAY</button>
                <button v-on:click="fold" class="btns">FOLD</button>
            </div>
            <div class="dealer">
                <textarea name="DEALER" id="dealerText" cols="10" rows="2" readonly></textarea>
            </div>
            <div class="btns2">
                <button v-on:click="deal" class="btns">HIT</button>
                <button v-on:click="newGame" class="btns">NEWGAME</button>
            </div>
            <div class="playerHand">
                <div class="pCard1" v-if="card6" v-on:click="flipper(6)">
                    <img :src="require(`~/assets/cards/${pHand[0]}.png`)" />
                </div>
                <div class="pCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="pCard2" v-if="card7">
                    <img :src="require(`~/assets/cards/${pHand[1]}.png`)" />
                </div>
                <div class="pCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="pCard3" v-if="card8">
                    <img :src="require(`~/assets/cards/${pHand[2]}.png`)" />
                </div>
                <div class="pCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="pCard4" v-if="card9">
                    <img :src="require(`~/assets/cards/${pHand[3]}.png`)" />
                </div>
                <div class="pCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
                <div class="pCard5" v-if="card10">
                    <img :src="require(`~/assets/cards/${pHand[4]}.png`)" />
                </div>
                <div class="pCard1" v-else>
                    <img :src="require(`~/assets/cards/flipped/0.png`)" />
                </div>
            </div>
        </div>
    </div>
</body>
</template>
<script>
export default {
    mounted() {
        this.newGame()
    },
    methods: {
        // game ideas:
        //  cards are rolled once at newgame and then left flipped,
        //  when clicked on they will flip over to their predetermined value
        //  maybe loser gets to pick oppponents first card
        //  goal is 23 not 21
        //  ace = 8 only
        //  only two buttons instead of four
        //  cute animations of my ogre guy holding a deck/hand of cards and reacting to plays
        //  REMOVE CARD FROM DECK AFTER ITS PUSHED
        hide() {
            // flip cards
            this.dealt = false
        },
        newGame() {
            // flip cards
            this.hide()
            // create deck
            this.mkDeck()
            // output message to dealer
            let dealText = document.getElementById("dealerText")
            this.message = "NEW GAME"
            dealText.innerHTML = this.message
        },
        roll(arg) {
            //simple rng roll
            let rng = Math.floor(Math.random() * arg)
            return rng
        },
        flipper(num) {
            let card = num
            this.card
        },
        mkDeck() {
            //init myDeck, suits, and ranks
            this.myDeck = []
            const suits = ["spade", "heart", "club", "diamond"]
            const ranks = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
            let selCard = String
            let selSuit = String
            let selRank = 0
            //put deck together
            for (let s = 0; s < this.suits.length; s++) {
                selSuit = suits[s]
                for (let r = 0; r < this.ranks.length; r++) {
                    selRank = ranks[r]
                    selCard = [selSuit, selRank]
                    this.myDeck.push(selCard)
                }
            }
        },
        deal() {
            this.playerDeal()
            this.opDeal()
            // display hand
            this.dealt = true
            // output message to dealer
            let dealText = document.getElementById("dealerText")
            this.message = "YOU HIT"
            dealText.innerHTML = this.message
        },
        // idea: track an compare all 10 rolls to prevent duplicates?
        playerDeal() {
            this.pHand = []
            // deal all of players hand
            let deck = this.myDeck.length
            if (deck >= 10) {
                for (let c = 0; c < 5; c++) {
                    let pCard = this.roll(this.myDeck.length)
                    let selCard = this.myDeck[pCard]
                    let pushr = selCard[0] + "/" + selCard[1]
                    this.pHand.push(pushr)
                    this.myDeck.splice(pCard, 1)
                }
            } else {
                this.mkDeck()
                this.playerDeal()
            }
        },
        opDeal() {
            this.opHand = []
            // deal all of ops hand
            for (let c = 0; c < 5; c++) {
                let opCard = this.roll(this.myDeck.length)
                let selCard = this.myDeck[opCard]
                let pushr = selCard[0] + "/" + selCard[1]
                this.opHand.push(pushr)
            }
        },
        stay() {
            this.hide()
            // output message to dealer
            let dealText = document.getElementById("dealerText")
            this.message = "YOU STAY"
            dealText.innerHTML = this.message
        },
        fold() {
            this.hide()
            // output message to dealer
            let dealText = document.getElementById("dealerText")
            this.message = "YOU FOLD"
            dealText.innerHTML = this.message
        }
    },
    data() {
        return {
            ranks: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13"],
            suits: ['spade', 'heart', 'club', 'diamond'],
            myDeck: Array,
            cards: ["heart8"],
            pHand: Array,
            opHand: Array,
            message: String,
            dealt: false,
            // card1: false,
            // card2: false,
            // card3: false,
            // card4: false,
            // card5: false,
            // card6: false,
            // card7: false,
            // card8: false,
            // card9: false,
            // card10: false,
            // dealtr: [
            //     [1, false],
            //     [2, false],
            //     [3, false],
            //     [4, false],
            //     [5, false],
            //     [6, false],
            //     [7, false],
            //     [8, false],
            //     [9, false],
            //     [10, false]
            // ],
        }
    },
}
</script>
<style scoped>
body {
    background-color: goldenrod;
}
.container {
    height: 96.6vh;
    width: 98.9vw;
    display: grid;
    grid-template-columns: 0.5fr 1.2fr 1.2fr 1.2fr 1.2fr 1.2fr 0.5fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    gap: 0px 0px;
    grid-auto-flow: row;
}
.container * {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    border: groove;
    border-color: red;
}
.opHand {
    grid-area: 1 / 2 / 2 / 7;
}
.playerHand {
    grid-area: 4 / 2 / 5 / 7;
}
.btns {
    height: 25%;
    width: 50%;
}
.btns2 {
    grid-area: 2 / 6 / 4 / 7;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
}
.btns1 {
    grid-area: 2 / 2 / 4 / 3;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
}
.dealer {
    grid-area: 2 / 3 / 4 / 6;
}
#dealerText {
    display: block;
    outline: none;
    resize: none;
    overflow: auto;
    height: 75%;
    width: 75%;
    font-size: 1000%;
    text-align: center;
}
.pCard1 {
    grid-area: 4 / 2 / 5 / 3;
}
.pCard2 {
    grid-area: 4 / 3 / 5 / 4;
}
.pCard3 {
    grid-area: 4 / 4 / 5 / 5;
}
.pCard4 {
    grid-area: 4 / 5 / 5 / 6;
}
.pCard5 {
    grid-area: 4 / 6 / 5 / 7;
}
.oCard1 {
    grid-area: 1 / 2 / 2 / 3;
}
.oCard2 {
    grid-area: 1 / 3 / 2 / 4;
}
.oCard3 {
    grid-area: 1 / 4 / 2 / 5;
}
.oCard4 {
    grid-area: 1 / 5 / 2 / 6;
}
.oCard5 {
    grid-area: 1 / 6 / 2 / 7;
}
</style>