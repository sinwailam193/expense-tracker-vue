<script setup>
import { ref, computed } from "vue";

import HeaderItem from "./components/HeaderItem.vue";
import BalanceItem from "./components/BalanceItem.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([
    { id: 1, text: "Flower", amount: -19.99 },
    { id: 2, text: "Salary", amount: 299.97 },
    { id: 3, text: "Book", amount: -10 },
    { id: 4, text: "Camera", amount: 150 }
]);

// get total
const total = computed(() =>
    transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0)
);

// get income
const income = computed(() =>
    transactions.value
        .filter((transaction) => transaction.amount > 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2)
);

// get expenses
const expenses = computed(() =>
    transactions.value
        .filter((transaction) => transaction.amount < 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2)
);

console.log(expenses, income);
</script>

<template>
    <HeaderItem />

    <div class="container">
        <BalanceItem :total="total" />
        <IncomeExpenses :income="income" :expenses="expenses" />
        <TransactionList :transactions="transactions" />
        <AddTransaction />
    </div>
</template>
