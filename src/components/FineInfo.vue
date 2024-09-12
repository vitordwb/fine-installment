<script setup>
import SiteIcon from './icons/IconSite.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import FineInfoItem from "@/components/FineInfoItem.vue";

defineProps({
  fineId: {
    type: Number,
    required: true
  },
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
})

</script>

<template>
  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Valor</template>

    <span style="text-transform: uppercase;">R$ 245,98</span>

  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <SiteIcon />
    </template>
    <template #heading>Local</template>

    <span style="text-transform: uppercase;">Rua Sao Sebastião, 360 – Chácara Santo Antonio</span>
  </FineInfoItem>

  <FineInfoItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Descrição</template>

    <span style="text-transform: uppercase;">AVANCAR O SINAL VERMELHO DO SEMAFORO OU DE PARADA</span>

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
