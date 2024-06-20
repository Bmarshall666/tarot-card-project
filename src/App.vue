<script setup>
import DisplayCard from './components/DisplayCard.vue';
</script>
<template>
  <div class="title">
    <h2>Welcome</h2>
    <div class="">Click to reveal your card</div>
  </div>
  <div class="container">
    <DisplayCard ref="cardRef" @card-info="cardInfo" />
    <button @click="$refs.cardRef.getTarot()">Retry</button>

  </div>

</template>

<style scoped>
h2 {
  margin: 0.5rem;
}

.container {
  position: relative;
  display: inline;
  align-items: center;
  justify-content: center;
  top: 50vh;
}

.title {
  position: relative;
  max-width: 15rem;
  text-align: center;
  left: calc(50vw - 120px);
  top: calc(50vh - 220px);
}

button {
  position: absolute;
  color: black;
  border-radius: 8px;
  border: 3px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #f9f9f9;
  cursor: pointer;
  transition: border-color 0.25s;
  left: calc(50vw - 40px);
  top: calc(25vh - 15px);
  -webkit-appearance: none;
}

button:hover {
  border-color: #8d90bb;
}

button:focus,
button:focus-visible {
  border-color: 4px auto #8d90bb;
}


@media (min-width: 370px) and (max-width: 768px) {
  .container {
    position: relative;
    display: inline;
    align-items: center;
    justify-content: center;
    top: calc(50vh - 100px);
  }
  

  button {
    position: absolute;
    color: black;
    border-radius: 8px;
    border: 3px solid transparent;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    font-family: inherit;
    background-color: #f9f9f9;
    cursor: pointer;
    transition: border-color 0.25s;
    left: calc(50vw - 40px);
    top: calc(25vh + 50px);
    -webkit-appearance: none;

  }
}




@media (min-width: 768px) and (max-width:2000px) {
  .container {
    position: relative;
    display: inline;
    align-items: center;
    justify-content: center;
    top: calc(50vh - 70px);
  }
  

  button {
    position: absolute;
    color: black;
    border-radius: 8px;
    border: 3px solid transparent;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    font-family: inherit;
    background-color: #f9f9f9;
    cursor: pointer;
    transition: border-color 0.25s;
    left: calc(50vw - 40px);
    top: calc(25vh + 10px);
    -webkit-appearance: none;

  }
}


</style>
