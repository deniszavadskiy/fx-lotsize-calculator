<script setup>
import { computed, ref } from "vue";

defineProps({
  msg: String,
});

const accountSize = ref(5000);
const risk = ref(1);
const lotCommission = ref(3);
const stopLossPips = ref(1);

const tickCost = computed(() => lotCommission.value / 10);
const riskInUSD = computed(() => (accountSize.value * risk.value) / 100);
const stopLossWithCommission = computed(
  () => tickCost.value + parseFloat(stopLossPips.value)
);

function getNumberWith2Digits(number) {
  return Math.round(number * 100) / 100;
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
  <b-container fluid="sm">
    <b-row cols="1" cols-md="2">
      <b-col>
        <label for="accSizeInput">Account size in $</label>
        <b-form-input
          id="accSizeInput"
          v-model="accountSize"
          placeholder="Account Size"
          type="number"
        ></b-form-input>
        <label for="risk">Risk in %</label>
        <b-form-input
          id="risk"
          v-model="risk"
          placeholder="Risk"
          type="number"
        ></b-form-input>
        <label for="commission">Commission in $</label>
        <b-form-input
          id="commission"
          v-model="lotCommission"
          placeholder="Commission"
          type="number"
          step="0.1"
        ></b-form-input>
      </b-col>
      <b-col>
        <p>Lots with commission: {{ lotsWithCommission }}</p>
        <p>Pips for 2R: {{ pipsFor2R }}</p>
        <p>Pips for 2R: {{ pipsFor3R }}</p>
        <label for="stopLossPips">Stop Loss in pips</label>
        <b-form-input
          id="stopLossPips"
          v-model="stopLossPips"
          placeholder="Stop loss pips"
          type="number"
          step="0.1"
        ></b-form-input>
      </b-col>
    </b-row>
  </b-container>
</template>

<style scoped></style>
