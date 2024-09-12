<script setup>

defineProps({
  driverName: {
    type: String,
    required: true
  },
  fineId: {
    type: Number,
    required: true
  }
})

</script>

<template>
  <span>fineId: {{ fineId }}</span>
  <div class="greetings">
    <h1 class="pink-kovi">Olá, {{ driverName }}</h1>
    <h3 class="pink-kovi">Infelizmente você tomou uma multa :(</h3>
    <h3>
      Receber uma multa nunca é legal, mas com nossas opções de parcelamento, fica mais fácil de resolver. Confira
      os detalhes e opções para você!
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
