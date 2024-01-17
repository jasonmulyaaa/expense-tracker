<template>
  <Header />
  <div class="container">
    <Balance :total="+total"/>

    <IncomeExpense :income="+income" :expense="+expense"/>
  <TransactionList :transaction="transaction" @deleteTransaction="handleTransactionDeleted"/>
  <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
</div>
</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification'

const toast = useToast()
const transaction = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transaction'))

  if(savedTransactions) {
    transaction.value = savedTransactions
  }
})
//get total balance
const total = computed(() => {
  return transaction.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

//get total income
const income = computed(() => {
  return transaction.value.filter((transaction) => transaction.amount > 0).reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2)
})

//get total expense
const expense = computed(() => {
  return transaction.value.filter((transaction) => transaction.amount < 0).reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2).substr(1)
})

const generateID = () => {
  return Math.floor(Math.random() * 1000000)
}

const handleTransactionSubmitted = (transactionData) => {
  transaction.value.push({
    id: generateID(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  
  saveTransactionsLocalStorage()

  toast.success('Transaksi ditambahkan!')
}

const handleTransactionDeleted = (id) => {
  transaction.value = transaction.value.filter((transaction) => transaction.id !== id)
  saveTransactionsLocalStorage()

  toast.success('Transaksi dihapus!')
}

const saveTransactionsLocalStorage = () => {
  localStorage.setItem('transaction', JSON.stringify(transaction.value))
}

</script>