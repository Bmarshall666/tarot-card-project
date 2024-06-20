<script setup>
import { reactive, ref, onMounted } from "vue";
import axios from "axios";

var clicked = ref(false)
var isFlipped = ref(false)

var resultState = reactive({
    name: "",
    number: "",
    arcana: "",
    meaning_rev: "",
    suit: "",
    img: "",
    Archetype: ""
})

var emit = defineEmits(["cardInfo"])

var onMounted(() =>{
    getTarot()
})

var getTarot = () => {
    var randCardNum = Math.floor(Math.random() * 58);
    var randMeaningNum = Math.floor(Math.random() * 3);

    axios.get('/tarot-images.json')
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

var isClicked = () => {
    clicked.value = true
    isFlipped.value = !isFlipped.value
}

defineExpose({ getTarot })



</script>

<template>
    <div class="card">
        <transition name="fade-card">
            <div v-if="isFlipped === false" class="inner-card">
                <img src="/cards/cardBack.jpg" @click="isClicked" class="cardBack">
            </div>
        </transition>

        <transition name="fade-card">
            <div v-if="isFlipped" class="inner-card">
                <img v-bind:src="'/cards/' + resultState.img" @click="isClicked" class="cardFront">
            </div>
        </transition>
        <div class="card-Info-Container">
            <transition name="fade">
                <div v-if="clicked" class="card-Info">
                    <div>{{ resultState.name }}</div>
                    <div>{{ resultState.meaning_rev }}</div>
                </div>
            </transition>
        </div>
    </div>

</template>


<style lang="scss" scoped>
.card {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
}

.cardFront {
    height: 25rem;
    width: 16rem;
    border-radius: 22px;
    max-width: 20.5rem;
}

.cardBack {
    max-width: 15.5rem;
    border-radius: 24px;
}

.inner-card {
    position: absolute;
    place-items: center;
    align-items: center;
}

.card-Info-Container {
    position: absolute;
    top: calc(18vh - 10px);
}

.card-Info {
    color: black;
    background-color: #f1f1f1;
    text-align: center;
    position: relative;
    min-width: 100vw;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 1.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

.fade-card-enter-active,
.fade-card-leave-active {
    transition: opacity 1.5s ease;
}

.fade-card-enter-from,
.fade-card-leave-to {
    opacity: 0;
}

@media (min-width: 360px) and (max-width: 768px) {
    .cardFront {
        height: 12.5rem;
        width: 8rem;
        border-radius: 22px;
        max-width: 20.5rem;
        object-position: 5px;
    }

    .cardBack {
        max-width: 7.75rem;
        border-radius: 24px;
    }

    .card-Info-Container {
        position: absolute;
        top: calc(18vh + 10px);
    }
}

@media (min-width: 768px) and (max-width:2000px) {
    .cardFront {
        height: 16.5rem;
        width: 10.5rem;
        border-radius: 22px;
        max-width: 20.5rem;
    }

    .cardBack {
        max-width: 10rem;
        border-radius: 15px;
    }

    .card-Info-Container {
        position: absolute;
        top: calc(18vh - 10px);
    }
}
</style>