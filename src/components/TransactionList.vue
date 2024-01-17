<!-- User Interface Component -->
<template>
    <h3>Riwayat</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transaction" 
        :key="transaction.id" 
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{ transaction.text }} <span>Rp.{{ transaction.amount }}</span><button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
        </li>
        <!-- <li class="minus">
          Cash <span>-$400</span><button class="delete-btn">x</button>
        </li>
        <li class="plus">
          Paycheck <span>+$400</span><button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<!-- Logical Functionality -->
<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['deleteTransaction'])
const props = defineProps({
    transaction: {
        type: Array,
        required: true,
    }
})

const deleteTransaction = (id) => {
    // console.log(id)
    emit('deleteTransaction', id)
}
</script>

<!-- Component Style -->
<style>

</style>