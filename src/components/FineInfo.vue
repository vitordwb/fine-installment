<script setup>
import SiteIcon from './icons/IconSite.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import FineInfoItem from "@/components/FineInfoItem.vue";
import {onMounted, ref} from "vue";
import axios from "axios";

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

    <span style="text-transform: uppercase;">'00020101021226940014br.gov.bcb.pix2572brcode-h.sandbox.starkinfra.com/v2/cobv/0d3904c33d544f2db07d58d96690503e5204000053039865802BR5920Kovi Tecnologia Ltda6009Sao Paulo62070503***6304BA65'</span>

  </FineInfoItem>

</template>
