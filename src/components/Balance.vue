<!-- User Interface Component -->
<template>
    <h4>
        Saldo Anda
    </h4>
    <h1 id="balance">
        Rp.{{ total }}
    </h1>
</template>

<!-- Logical Functionality -->
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    total: {
        type: Number,
        required: true
    }
})
</script>

<!-- Component Style -->
<style>

</style>