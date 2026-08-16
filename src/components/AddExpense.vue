<template>
    <div class="fixed inset-0 bg-(--color-background)/50">
        <div class="border border-(--color-border-icon) h-auto mx-2 my-25 p-6 bg-white rounded-4xl">
            <div class="flex justify-between ">
                <div></div>
                <h2 class="mt-5 mb-6 flex justify-center text-2xl font-bold">ADD Expense</h2>
                <X @click="emit('close')" class="mt-5 text-(--color-text-primary) hover:text-(--color-primary-green)" size="30"/>
            </div>
            <form @submit.prevent="addExpense" class="flex flex-col gap-6">
                <div class="flex flex-col gap-2">
                    <p class="text-xl">Description:</p>
                    <input v-model="description" class="border w-full px-2 py-4 rounded-2xl" type="text" placeholder="e.g  Lunch,Bus,Coffee">
                </div>
                <div class="flex flex-col gap-2">
                    <p class="text-xl">Amount (MMK):</p>
                    <input v-model="amount" class="border w-full px-2 py-4 rounded-2xl" type="text" placeholder="e.g. 5000">
                </div>
                <div class="flex flex-col gap-2">
                    <p class="text-xl">Date:</p>
                    <input v-model="date" class="border w-full px-2 py-4 rounded-2xl" type="date" value="Aug 11, 2026">
                </div>
                <button type="submit" class="w-full bg-(--green-color-primary) text-white py-4 rounded-2xl hover:bg-(--green-hover-color-primary) shadow-xl my-5 text-xl">Add Expense</button>
            </form> 
        </div>
    </div>
</template>
<script setup>
    import { 
        X,
    } from '@lucide/vue';

import { ref,computed } from "vue";

const emit = defineEmits([
    'close',
    'expense-added',
]);
const description = ref('');
const amount = ref('');
const date = ref('');
const showAlert = ref(false);

function addExpense(){
    if(description.value === '' || amount.value === ''){
        alert('Please fill all')
        return;
        }else{
            const Expense = {
            id: Date.now(),
            description: description.value,
            amount: Number(amount.value ),
            date: date.value
        };
        emit('expense-added',Expense)
    };
};
</script>