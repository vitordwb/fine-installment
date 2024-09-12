<script setup>
import { useRoute } from "vue-router";
import {onMounted, ref} from "vue";
import GreetingMessage from "@/components/GreetingMessage.vue";
import FineInfo from "@/components/FineInfo.vue";
import axios from 'axios'

const route = useRoute();
const fineId = route.params.fineId;

const fineData = ref('')
const driverName = ref('');
const fineAmount =  ref('');
const finePoints =  ref('');
const fineSite =  ref('');
const fineDescription =  ref('');
const fineDateHour =  ref('');
const fineStatus =  ref('');

const fetchFineData = async () => {
  try {
    const response = await axios.get('https://mocki.io/v1/7055eb5a-447b-4e5c-8a8b-51164c988714');
    fineData.value = response.data

    driverName.value = fineData.value.name
    fineAmount.value = fineData.value.amount
    finePoints.value = fineData.value.issue_points
    fineSite.value = fineData.value.issue_location
    fineDescription.value = fineData.value.description
    fineDateHour.value = fineData.value.issued_at
    fineStatus.value = fineData.value.status

    console.log(fineData.value);
  } catch (error) {
    console.error('Erro ao buscar dados:', error);
  }
};

onMounted(() => {
  fetchFineData();
});

</script>

<template>
  <header>
    <img alt="Kovi logo" class="logo" src="@/assets/logo.svg" width="120" height="125" />

    <div class="wrapper">
      <GreetingMessage :driver-name=driverName />
    </div>
  </header>
  <main>
    <FineInfo :fine-amount="fineAmount" :fine-site="fineSite" :fine-description="fineDescription" />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
