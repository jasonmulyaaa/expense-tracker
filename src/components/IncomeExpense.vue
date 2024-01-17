<!-- User Interface Component -->
<template>
  <div class="inc-exp-container">
    <div>
        <h4>
            Pendapatan
        </h4>
        <p id="money-plus" class="money-plus">+Rp.{{ income }}</p>
    </div>
    <div>
        <h4>Pengeluaran</h4>
        <p id="money-minus" class="money-minus">-Rp.{{ expense }}</p>
    </div>
  </div>
</template>

<!-- Logical Functionality -->
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense: {
        type: Number,
        required: true
    }
})
</script>

<!-- Component Style -->
<style>

</style>