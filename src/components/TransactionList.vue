<script setup>
import { defineProps } from "vue";

defineProps({
    transactions: {
        type: Array,
        required: true
    }
});
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li
            v-for="transaction in transactions"
            :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{ transaction.text }} <span>${{ transaction.amount }}</span>
            <button class="delete-btn">x</button>
        </li>
    </ul>
</template>
