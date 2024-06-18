<script setup>
import { reactive, ref } from "vue";
import axios from "axios"


const randCardNum = Math.floor(Math.random() * 58);
const randMeaningNum = Math.floor(Math.random() * 3);

axios.get('tarot-images.json')
  .then((data) => {
    resultState.name = data.data.cards[randCardNum].name
    resultState.number = data.data.cards[randCardNum].number
    resultState.arcana = data.data.cards[randCardNum].arcana
    resultState.meaning_rev = data.data.cards[randCardNum].meanings.light[randMeaningNum]
    resultState.suit = data.data.cards[randCardNum].suit
    resultState.img = data.data.cards[randCardNum].img
    resultState.Archetype = data.data.cards[randCardNum].Archetype

  });

const clicked = ref(false)
const isFlipped = ref(false)

const resultState = reactive({
  name: "",
  number: "",
  arcana: "",
  meaning_rev: "",
  suit: "",
  img: "",
  Archetype: ""
})

const getTarot = () => {
  const randCardNum = Math.floor(Math.random() * 58);
  const randMeaningNum = Math.floor(Math.random() * 3);

  axios.get('tarot-images.json')
    .then((data) => {
      resultState.name = data.data.cards[randCardNum].name
      resultState.number = data.data.cards[randCardNum].number
      resultState.arcana = data.data.cards[randCardNum].arcana
      resultState.meaning_rev = data.data.cards[randCardNum].meanings.light[randMeaningNum]
      resultState.suit = data.data.cards[randCardNum].suit
      resultState.img = data.data.cards[randCardNum].img
      resultState.Archetype = data.data.cards[randCardNum].Archetype

    });
  clicked.value = false
  isFlipped.value = false
}

const isClicked = () => {
  clicked.value = true
  isFlipped.value = !isFlipped.value
  console.log("hello")
}

</script>
<template>
  <h2>Welcome</h2>
  <div>Click the card to reveal your card</div>
  <section>
    <div class="card">
      <div class="inner-card">
        <img v-if="isFlipped" v-bind:src="'/src/assets/cards/' + resultState.img" @click="isClicked" class="cardFront">
        <img v-if="isFlipped === false" src="/src/assets/cards/cardBack.jpg" @click="isClicked" class="cardBack">
      </div>
      <div class="card-info">
        <transition name="fade">
          <div v-if="clicked">
            <div>{{ resultState.name }}</div>
            <div>{{ resultState.meaning_rev }}</div>
          </div>
        </transition>
      </div>
    </div>
    <button class="retry" @click="getTarot">Retry</button>
  </section>
</template>

<style scoped>
.card {
  padding: 5px;
}

.card-info {
  color: black;
  background-color: #f1f1f1;
  min-width: 5rem;
  min-height: 5rem;
  border-radius: 26px;
  padding: 0;
  margin: 0;
  font-weight: 500;
  text-align: center;
  align-items: center;
}

.cardFront {
  max-height: 33.6rem;
  width: 24rem;
  border-radius: 22px;
  max-width: 20.5rem;
  object-position: 5px;
}

button {
  margin: .3rem;
}

.cardBack {
  max-width: 20.5rem;
  border-radius: 24px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
