<script setup>
import { useRoute } from "vue-router";
import { onMounted, ref } from "vue";
import GreetingMessage from "@/components/GreetingMessage.vue";
import FineInfo from "@/components/FineInfo.vue";
import axios from 'axios'

const route = useRoute();
const fineId = route.params.fineId;

const fineData = ref('')
const driverName = ref('')
const fineAmount =  ref(0)
const finePoints =  ref(0)
const fineSite =  ref('')
const fineDescription =  ref('')
const fineDateHour =  ref('')
const fineStatus =  ref('')
const fineBooking =  ref('')
const fineDriver =  ref('')

const fetchFineData = async () => {
  try {
    const response = await axios.get('https://mocki.io/v1/7055eb5a-447b-4e5c-8a8b-51164c988714');
    fineData.value = response.data

    driverName.value      = fineData.value.name
    fineAmount.value      = response.data.amount
    finePoints.value      = fineData.value.issue_points
    fineSite.value        = fineData.value.issue_location
    fineDescription.value = fineData.value.description
    fineDateHour.value    = fineData.value.issued_at
    fineStatus.value      = fineData.value.status
    fineBooking.value      = response.data.booking
    fineDriver.value      = fineData.value.driver

  } catch (error) {
    console.error('Erro ao buscar dados da multa:', error);
  }
};

const fetchInstallmentData = async () => {

  const fineAmountInt = 235

  // console.log('fineAmountInt', fineAmountInt)
  const data = {
    "id": "a226b917-578b-4464-bbb1-3626d6e8ac86",
    "dt_partition": "2024-09-12",
    "__kafka_metadata_id": "None",
    "__kafka_metadata_offset": 18853904,
    "__kafka_metadata_partition": 0,
    "__kafka_metadata_timestamp": "2024-09-12 20:27:41.028",
    "ait": "PMC3377779",
    "amount": 293.47,
    "amount_charged": 352.16,
    "booking": "19bf4cc4-efb9-4608-8433-1d68a757dd7e",
    "car": "6948d996-1160-495b-9bd7-bfd3339b6ee5",
    "charged_at": "2024-06-12 17:35:47.000",
    "checked_at": "2024-09-12 20:27:16.000",
    "created_at": "2024-06-12 17:21:21.000",
    "description": "AVANCAR O SINAL VERMELHO DO SEMAFORO",
    "driver": "c5676bd1-cdc9-40d1-aeca-a3bea4fd7e4a",
    "expired_at": "2024-09-09 00:00:00.000",
    "fine_url": "None",
    "imposed_at": "2024-09-12 20:27:17.000",
    "ingested_at": "None",
    "is_notification": 0,
    "issue_city": "SAO PAULO",
    "issue_code": "605-01",
    "issue_country": "BR",
    "issue_id": "19190790",
    "issue_indicate_limit": "2024-07-16 00:00:00.000",
    "issue_institution": "271070 / PREFEITURA MUNICIPAL DE SAO PAULO - SP (DEPARTAMENTO DE OPERACAO DO SISTEMA VIARIO - DSV)",
    "issue_location": "RUA GLICERIO                           X RUA BARAO DE IGUAPE                      , D",
    "issue_points": 7,
    "issue_state": "SP",
    "issued_at": "2024-05-20 10:17:00.000",
    "issued_at_tz": "-03:00",
    "metadata_ingestion_order": "2024-09-12 20:27:22__4__2024-09-12T20:27:22.136000",
    "metadata_kinesis_received_at": "2024-09-12 20:27:22.136",
    "metadata_operation": "update",
    "metadata_partition": "None",
    "metadata_partition_key_type": "schema-table",
    "metadata_record_type": "data",
    "metadata_schema_name": "rental",
    "metadata_table_name": "fines",
    "metadata_timestamp": "2024-09-12 20:27:22.000",
    "metadata_transaction_id": 143890047007226,
    "metadata_transforms_started_at": "2024-09-12 20:27:39.938",
    "notified_at": "2024-08-22 19:45:28.000",
    "parent_ait": "None",
    "region_city": "None",
    "region_country": "None",
    "region_group": "None",
    "region_state": "None",
    "regulatory_fees_due_date": "None",
    "snapshot_at": "None",
    "status": "PAID",
    "status_indication": "Enviado ao órgão",
    "transaction": "0e6da6f2-f46e-40a4-8bc1-a6562939538a",
    "updated_at": "2024-09-12 20:27:17.000",
    "year": "None",
    "condition_field": "2024-09-12 20:27:22__4__2024-09-12T20:27:22.136000",
    "metadata_operation_1": "update",
    "name": "CAROLINA ALVES DA SILVA EPIFANIO"
  }

  const params = {
    booking_id: data.booking,
    fine_id: data.id,
    driver_id: data.driver,
    amount: 123,
  }

  try {
    console.log()
    const response2 = await axios.post(
        `http://payments-wizard.dev.kovi.internal/api/v1/kobaya/fines/${fineId}/invoices`
        ,params
    );

    installmentData.value = response2.data
    console.log('xd', response.data);

    console.log(installmentData.value);
  } catch (error) {
    console.error('Erro ao buscar dados de parcelamento:', error);
  }
};

onMounted(() => {
  fetchFineData()
  fetchInstallmentData()
});

</script>

<template>
  <header>
    <img alt="Kovi logo" class="logo" src="@/assets/logo.svg" width="120" height="125" />

    <div class="wrapper">
      <GreetingMessage driver-name="Cleverson Soares" />
    </div>
  </header>
  <main>
    <FineInfo :fine-amount="fineAmount"
              :fine-site="fineSite"
              :fine-description="fineDescription"
              :fine-date-hour="fineDateHour"
              :fine-id="fineId"
              :fine-booking="fineBooking"
    />
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
