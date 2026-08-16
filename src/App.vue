
<template >
    <div class="bg-(--color-background) pt-5" >
        <header class="flex justify-between max-w-5xl px-4 items-center">
            <h1 class="text-3xl font-bold text-(--color-text-primary)" >Monthly Tracker</h1>
            <Settings :size="30"/>
        </header>
        <section class="mt-6 px-4">
            <div class="flex items-center gap-3 md:gap-10 justify-between md:justify-start ">
                <button @click="openExpense"  class="flex items-center gap-2 bg-[#2E7D32] text-white px-5 py-3 rounded-2xl font-medium shadow-md hover:bg-[#256628] transition-colors">
                    <span class="text-lg leading-none">+</span>
                    <span>Add Expense</span>
                </button>

                <!-- ၂။ ဒုတိယ History ခလုတ် (အဖြူရောင်နောက်ခံ၊ မီးခိုးရောင်အနားသတ်) -->
                <button class="flex items-center gap-2 bg-white text-[#212121] px-4 py-2.5 rounded-2xl font-medium border border-[#9E9E9E] shadow-sm hover:bg-gray-50 transition-colors">
                    <span class="text-sm text-[#9E9E9E]">🕒</span>
                    <span>History</span>
                </button>

                <!-- ၃။ တတိယ Today ခလုတ် (အစိမ်းရောင်အနားသတ်) -->
                <button class="bg-white text-[#2E7D32] px-5 py-2.5 rounded-2xl font-medium border border-[#2E7D32] shadow-sm hover:bg-green-50 transition-colors">
                    Today
                </button>
            </div>
            <div class="bg-white border-2  border-(--color-phone-border) rounded-2xl shadow-[0-4px-12px-rgba(0,0,0,0,0.05)] p-5 mt-4 h-140 max-w-5xl ">

               <div class="text-xl" >{{ displayDate }}<br><span class="text-lg text-(--color-text-secondary)">{{ displayDay }}</span></div>
               <div class="mt-7 pb-4  flex flex-col gap-3 justify-center text-center border-b-1 border-(--color-border-icon)">
                    <span class="text-2xl">Today's Spending  </span>
                    <span class="text-(--green-color-primary) text-4xl">{{ totalExpenseData }} MMK</span>
                </div>
                <div class="border-b border-b-(--color-border-icon) py-4 h-70 flex flex-col gap-3 ">
                    <div v-for="data in ExpenseRealData" :key="data.id" class="flex justify-between text-md">
                       <span> {{ data.description }}</span>
                       <div class="flex justify-between gap-5">
                        <span class="text-lg">{{ data.amount }} MMK</span>
                        <Pencil class="text-(--color-text-secondary)"/>
                        <Trash2 @click="deleteExpense(ExpenseRealData.id)" class="text-(--color-delete-icon)"/>
                       </div>
                       
                    </div>
                </div>
                <div class="flex justify-between py-4">
                    <p class="text-xl">Total</p>
                    <span class="text-(--green-color-primary)">{{ totalExpenseData }} MMK</span>
                </div>
            </div>
        </section>
        <footer class="shrink-0 border-t border-t-(--color-border-icon) flex justify-between mt-7 px-5 pt-3 ">
            <div class="flex flex-col items-center hover:text-(--color-primary-green)">
                <House :size="30"/>
                <span>Home</span>
            </div>
            <div class="flex flex-col items-center">
                <Clock :size="30"/>
                <span>History</span>
            </div>
            <div class="flex flex-col items-center">
                <Summary :size="30" />
                <span>Summary</span>
            </div>
        </footer>
        <AddExpense 
            v-if="showExpense"
            @close="closeExpense"
            @expense-added="handleExpense" 
        /> 
    </div>
</template>
<script setup>
import AddExpense from './components/AddExpense.vue'
import { ref,computed,onMounted } from "vue";
    import { 
        House,
        Summary,
        Clock,
        Settings,
        Pencil,
        Trash2,
    } from '@lucide/vue';

const showExpense = ref(false);
    function openExpense(){
        showExpense.value = true;
    };
    function closeExpense(){
        showExpense.value = false;
    };

const ExpenseRealData = ref([]);
    function handleExpense(Expense){//getting expense data from child 
        ExpenseRealData.value.push(Expense);
        localStorage.setItem(
            'Expense',
            JSON.stringify(ExpenseRealData.value)
        );
    };
    onMounted(() => {
  const savedExpenses = localStorage.getItem('Expense');

  if (savedExpenses) {
    ExpenseRealData.value = JSON.parse(savedExpenses);
  };
});

// for Date
const selectedDate = ref(new Date());
const displayDate = computed(() => {
    return selectedDate.value.toLocaleDateString('en-US',{
        month: 'long',
        day: 'numeric',
        year: 'numeric'
    });
});
const displayDay = computed(()=>{
    return selectedDate.value.toLocaleDateString('en-US',{
        weekday: 'long'
    });
});

// total expense data 
const totalExpenseData = computed(() => {
    return ExpenseRealData.value.reduce((total,Expense) => {
        return total + Expense.amount;
    },0); 
});

// delete button 
function deleteExpense(id){
    
}

</script>
