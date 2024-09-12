<script setup>
import SiteIcon from './icons/IconSite.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import FineInfoItem from "@/components/FineInfoItem.vue";

defineProps({
  fineAmount: {
    type: Number,
    required: false
  },
  fineSite: {
    type: Number,
    required: false
  },
  fineDescription: {
    type: Number,
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

</script>

<template>
  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Valor</template>

    <span style="text-transform: uppercase;">R$ {{ fineAmount }}</span>

  </FineInfoItem>

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

    <span style="text-transform: uppercase;">{{ fineSite }}</span>
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
      <EcosystemIcon />
    </template>
    <template #heading>Parcelas</template>

    <select v-model="selectedInstallment">
      <option v-for="option in installmentOptions" :key="option" :value="option">
        {{ option }}x
      </option>
    </select>
  </FineInfoItem>

</template>
