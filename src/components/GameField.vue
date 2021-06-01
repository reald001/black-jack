<template>
  <div class="field">
    <div class="player-hand">
      <Card v-for="card of playerCards" :key="card" :card="card" />
    </div>
    <p>Your score: {{ playerScore }}</p>
    <button @click="takeCard" class="take-card btn">TAKE CARD</button>
    <!-- <button @click="endTurn" class="end-turn btn">ENOUTH</button> -->
  </div>
</template>

<script>
import Card from "./Card";
export default {
  name: "GameField",
  components: {
    Card,
  },

  data() {
    return {
      cards: {
        "T-p": 11,
        "T-c": 11,
        "T-k": 11,
        "T-b": 11,
        "2-b": 2,
        "3-b": 3,
        "4-b": 4,
        "5-b": 5,
        "6-b": 6,
        "7-b": 7,
        "8-b": 8,
        "9-b": 9,
        "10-b": 10,
        "J-b": 10,
        "Q-b": 10,
        "K-b": 10,
      },
      cardsInDeck: {},
      playerCards: [],
      playerScore: 0,
      gameOver: false
    };
  },

  methods: {
    randomCard(cards) {
      let keys = Object.keys(cards);
      const card = keys[(keys.length * Math.random()) << 0];
      delete cards[card];
      return card;
    },
    setScore() {
      this.playerScore = 0
      for (let card of this.playerCards) {
        this.playerScore += this.cards[card];
      }
    },
    if22(){
      this.reduceTuzes()
      this.gameOver = false
      return
    },
    reduceTuzes(){    //the most understandable solution
      if(this.playerCards.includes("T-c") && this.cards["T-c"] === 11){
        this.cards["T-c"] = 1
        this.setScore()
        return
      }
      if(this.playerCards.includes("T-b") && this.cards["T-b"] === 11){
        this.cards["T-b"] = 1
        this.setScore()
        return
      }
      if(this.playerCards.includes("T-k") && this.cards["T-k"] === 11){
        this.cards["T-k"] = 1
        this.setScore()
        return
      }
      if(this.playerCards.includes("T-p") && this.cards["T-p"] === 11){
        this.cards["T-p"] = 1
        this.setScore()
        return
      }
      
      this.gameOver = true
      return
    },
    takeCard(){
      if(this.gameOver) return

      this.playerCards.push(this.randomCard(this.cardsInDeck));
      this.setScore()
      if(this.playerScore > 21){
        this.reduceTuzes()
      }
    },
    // endTurn(){

    // }
  },

  mounted() {
    this.cardsInDeck = Object.assign({}, this.cards);

    this.playerCards.push(this.randomCard(this.cardsInDeck));
    this.playerCards.push(this.randomCard(this.cardsInDeck));
    this.if22()
    this.setScore();
  },
};
</script>

<style scoped lang="scss">
.player-hand {
  display: flex;
  justify-content: space-between;
  width: max-content;
  margin: 0 auto;
}
</style>
