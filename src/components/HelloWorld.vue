<script setup>
import { computed, ref } from "vue";

defineProps({
  msg: String,
});

const accountSize = ref(10000);
const risk = ref(1);
const lotCommission = ref(3);
const stopLossPips = ref(1);

const lotsWithCommission = computed(() => {
  const tickCost = lotCommission.value / 10;
  const riskInUSD = (accountSize.value * risk.value) / 100;
  const stopLossWithCommission = tickCost + parseFloat(stopLossPips.value);
  const lots = (riskInUSD / stopLossWithCommission / 0.1) * 0.01;

  return Math.round(lots * 100) / 100 ;
});
</script>

<template>
  <b-container fluid>
    <b-row>
      <b-col>
        <label for="stopLossPips">Stop Loss in pips</label>
        <b-form-input
          id="stopLossPips"
          v-model="stopLossPips"
          placeholder="Stop loss pips"
          type="number"
          step="0.1"
        ></b-form-input>
      </b-col>
      <b-col>
        <label for="accSizeInput">Account size in $</label>
        <b-form-input
          id="accSizeInput"
          v-model="accountSize"
          placeholder="Account Size"
          type="number"
        ></b-form-input>
      </b-col>
      <b-col>
        <label for="risk">Risk in %</label>
        <b-form-input
          id="risk"
          v-model="risk"
          placeholder="Risk"
          type="number"
        ></b-form-input>
      </b-col>
      <b-col>
        <label for="commission">Commission in $</label>
        <b-form-input
          id="commission"
          v-model="lotCommission"
          placeholder="Commission"
          type="number"
        ></b-form-input>
      </b-col>
    </b-row>
  </b-container>

  <p>{{ lotsWithCommission }}</p>
</template>

<style scoped></style>
