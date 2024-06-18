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
}

</script>
<template>
  <div class="title">
    <h2>Welcome</h2>
    <div>Click to reveal your card</div>
  </div>
  <section>
    <div class="card">

      <transition name="fade-card">
        <div v-if="isFlipped === false" class="inner-card">
          <img src="/src/assets/cards/cardBack.jpg" @click="isClicked" class="cardBack">
        </div>
      </transition>

      <transition name="fade-card">
        <div v-if="isFlipped" class="inner-card">
          <img v-bind:src="'/src/assets/cards/' + resultState.img" @click="isClicked" class="cardFront">
        </div>
      </transition>

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
h2 {
  margin: 1vh;
}

.title {
  margin: 5vh;
  
}

.card {
  position: relative;
  padding: 5px;
  display: flex;
  place-items: center;
  align-items: center;
}

.inner-card {
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 15vh;
  left: 0;
  right: 0;
  text-align: center;

}

.card-info {
  color: black;
  background-color: #f1f1f1;
  min-width: 30rem;
  min-height: 5rem;
  border-radius: 26px;
  padding: 0;
  margin: 0;
  text-align: center;
  align-items: center;
  margin-top: 45vh;
  position: relative;
}

.cardFront {
  max-height: 25rem;
  width: 16rem;
  border-radius: 22px;
  max-width: 20.5rem;
  object-position: 5px;
}

button {
  margin: .3rem;
}

.cardBack {
  max-width: 15.5rem;
  border-radius: 24px;
}

.fade-card-enter-active,
.fade-card-leave-active {
  transition: opacity 1.5s ease;
}

.fade-card-enter-from,
.fade-card-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
