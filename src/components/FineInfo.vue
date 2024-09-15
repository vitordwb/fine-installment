<script setup>
import SiteIcon      from './icons/IconSite.vue'
import ToolingIcon   from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import FineInfoItem  from '@/components/FineInfoItem.vue';
import { ref }       from 'vue';

defineProps({
  barCode:{
    type: String,
    required: false,
  },
  fineAmount: {
    type: String,
    required: false
  },
  fineBooking: {
    type: String,
    default: false
  },
  fineId: {
    type: String,
    required: false
  },
  fineSite: {
    type: String,
    required: false
  },
  fineDescription: {
    type: String,
    required: false
  },
  finePoints: {
    type: Number,
    required: false
  },
  fineDateHour: {
    type: String,
    required: false
  },
  fineStatus: {
    type: String,
    required: false
  },

})

const showBanner = ref(false);
const bannerMessage = ref('');

const copyToClipboard = () => {
  navigator.clipboard.writeText(barcode.value)
      .then(() => {
        showBanner.value = true;
        bannerMessage.value = 'Código de barras copiado!';

        setTimeout(() => {
          showBanner.value = false;
        }, 10000);
      })
      .catch(err => {
        console.error('Falha ao copiar o código de barras:', err);
      });
};

const formatDate = (dateString) => {
  if (!dateString) return '';

  const date = new Date(dateString);
  const day = String(date.getDate()).padStart(2, '0')
  const month = String(date.getMonth() + 1).padStart(2, '0')
  const year = date.getFullYear()
  const hours = String(date.getHours()).padStart(2, '0')
  const minutes = String(date.getMinutes()).padStart(2, '0')

  return `${day}/${month}/${year} ${hours}:${minutes}`;
};

const installmentData = ref('')

const selectedInstallment = ref(1);
const installmentOptions = ref([1, 2, 3, 4]);

</script>

<template>

  <FineInfoItem>
    <template #icon>
      <SiteIcon />
    </template>
    <template #heading>Local</template>

    <span style="text-transform: uppercase;">{{ fineSite }}</span>
  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <SiteIcon />
    </template>
    <template #heading>Data & Hora</template>

    <span style="text-transform: uppercase;">{{ formatDate(fineDateHour) }}</span>
  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Descrição</template>

    <span style="text-transform: uppercase;">{{ fineDescription }}</span>
  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Valor</template>

    <span style="text-transform: uppercase;">R$ {{ fineAmount }}</span>

  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <EcosystemIcon />
    </template>
    <template #heading>Parcelas</template>

    <select v-model="selectedInstallment">
      <option v-for="option in installmentOptions" :key="option" :value="option">
        {{ option }}x
      </option>
    </select>
  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Código de Barras</template>

    <div>
      <span style="text-transform: uppercase;">{{ barCode }}</span>
      <br>
      <button @click="copyToClipboard" style="margin-left: 1rem;">Copiar</button>
    </div>
  </FineInfoItem>

</template>

<style scoped>
button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.banner {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  background-color: #28a745;
  color: white;
  padding: 1rem 2rem;
  border-radius: 0.25rem;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  font-size: 1rem;
  text-align: center;
}
</style>
