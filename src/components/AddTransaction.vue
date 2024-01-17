<!-- User Interface Component -->
<template>
<h3>Tambah Transaksi baru</h3>
<form id="form" @submit.prevent="onSubmit">
  <div class="form-control">
    <label for="text">Teks</label>
    <input type="text" id="text" placeholder="Enter text..." v-model="text"/>
  </div>
  <div class="form-control">
    <label for="amount">
      Jumlah <br />
      ("-" = pengeluaran, "+" = pendapatan)
    </label>
    <br>
    <span style="font-size: 16px; opacity: 0.5;">Contoh: -500000</span>
    <input type="text" id="amount" placeholder="Enter amount..." v-model="amount"/>
  </div>
  <button class="btn">Tambah Transaksi</button>
</form>
</template>

<!-- Logical Functionality -->
<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification'

const text = ref('')
const amount = ref('')
const toast = useToast()

const emit = defineEmits(['transactionSubmitted'])

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Form harus diisi!')
    return
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit('transactionSubmitted', transactionData)
  text.value = ''
  amount.value = ''
}
</script>

<!-- Component Style -->
<style>

</style>