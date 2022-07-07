<script setup>
import { computed, ref, watch, onMounted } from "vue";

const accountSize = ref(5000);
const risk = ref(1);
const lotCommission = ref(3);
const stopLossTicks = ref(50);

const tickCost = computed(() => lotCommission.value / 10);
const riskInUSD = computed(() => (accountSize.value * risk.value) / 100);
const stopLossPips = computed(() => stopLossTicks.value / 10);
const stopLossWithCommission = computed(
  () => tickCost.value + stopLossPips.value
);

watch(accountSize, (newValue) => {
  localStorage.setItem("accountSize", newValue);
});

watch(risk, (newValue) => {
  localStorage.setItem("risk", newValue);
});

watch(lotCommission, (newValue) => {
  localStorage.setItem("lotCommission", newValue);
});

onMounted(() => {
  accountSize.value = localStorage.getItem("accountSize") || 5000;
  risk.value = localStorage.getItem("risk") || 1;
  lotCommission.value = localStorage.getItem("lotCommission") || 3;
});

function getNumberWith2Digits(number) {
  return Math.round(number * 100) / 100;
}

function onStopSizeInputFocus() {
  stopLossTicks.value = '';
}

const lotsWithCommission = computed(() => {
  const lots = (riskInUSD.value / stopLossWithCommission.value / 0.1) * 0.01;

  return getNumberWith2Digits(lots);
});

function getPipsForNR(rewardNumber) {
  return getNumberWith2Digits(
    stopLossPips.value * rewardNumber +
    tickCost.value * rewardNumber +
    tickCost.value
  );
}

const pipsFor2R = computed(() => getPipsForNR(2));
const pipsFor3R = computed(() => getPipsForNR(3));
</script>

<template>
  <b-container fluid="sm" class="calculator">
    <b-row cols="1" cols-md="2">
      <b-col class="
          d-flex
          flex-column
          justify-content-between
          text-left
          config-column
        ">
        <b-container class="p-0 d-flex align-items-center">
          <label for="accSizeInput" class="flex-1">Account size in $</label>
          <b-form-input min="0" class="flex-1" size="lg" id="accSizeInput" v-model="accountSize"
            placeholder="Account Size" type="number" inputmode="numeric"></b-form-input>
        </b-container>
        <b-container class="p-0 d-flex align-items-center">
          <label for="risk" class="flex-1">Risk in %</label>
          <b-form-input min="0" class="flex-1" size="lg" id="risk" v-model="risk" placeholder="Risk" type="number"
            inputmode="decimal">
          </b-form-input>
        </b-container>
        <b-container class="p-0 d-flex align-items-center">
          <label for="commission" class="flex-1">Commission in $</label>
          <b-form-input min="0" class="flex-1" size="lg" id="commission" v-model="lotCommission"
            placeholder="Commission" type="number" step="0.1" inputmode="decimal"></b-form-input>
        </b-container>
      </b-col>
      <b-col class="d-flex flex-column justify-content-between config-column">
        <b-container class="p-0 d-flex flex-column align-items-between">
          <p class="d-flex justify-content-between calculation-result">
            Lots with commission:
            <span class="font-weight-bold">{{ lotsWithCommission }}</span>
          </p>

          <p class="d-flex justify-content-between calculation-result">
            Pips for 2R: <span class="font-weight-bold">{{ pipsFor2R }}</span>
          </p>
          <p class="d-flex justify-content-between calculation-result mb-0">
            Pips for 3R: <span class="font-weight-bold">{{ pipsFor3R }}</span>
          </p>
        </b-container>
        <b-container class="p-0 d-flex align-items-center">
          <label for="stopLossTicks" class="flex-1 text-left">Stop Loss(ticks)</label>
          <b-form-input min="10" class="flex-1" size="lg" id="stopLossTicks" v-model="stopLossTicks"
            placeholder="Stop loss pips" type="number" inputmode="numeric" @focus="onStopSizeInputFocus">
          </b-form-input>
        </b-container>
      </b-col>
    </b-row>
  </b-container>
</template>

<style scoped>
.calculator {
  height: 100%;
}

.flex-1 {
  flex: 1;
}

.text-left {
  text-align: left;
}

:deep(.form-control) {
  border: none;
  color: #fff;
  background-color: #36373b;
}

:deep(.form-control:focus) {
  color: #fff;
  background-color: #2c2c2c;
  box-shadow: 0 0 0 0.25rem rgb(0 199 180 / 25%);
}

:deep(.container) {
  max-width: 720px;
}

@media (min-width: 768px) {
  .container-sm {
    max-width: 720px !important;
  }
}

.calculation-result {
  font-weight: bold;
  color: #00c7b4 !important;
}

.calculation-result span {
  font-size: 1.5rem;
}

.config-column .container {
  margin: 1rem 0;
}

.font-weight-bold {
  font-weight: bold;
}
</style>


