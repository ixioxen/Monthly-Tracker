<template>

    <div
        class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 px-4"
    >

        <!-- Delete Box -->
        <div
            class="w-full max-w-sm bg-white rounded-3xl p-6 shadow-2xl"
        >

            <!-- Title -->
            <h2 class="text-2xl font-bold text-(--color-text-primary)">
                Delete Expense?
            </h2>


            <!-- Message -->
            <p class="mt-3 text-(--color-text-secondary)">
                Are you sure you want to delete this expense?
                This action cannot be undone.
            </p>


            <!-- Buttons -->
            <div class="flex gap-3 mt-7">

                <!-- Cancel -->
                <button
                    @click="emit('close')"
                    class="flex-1 py-3 rounded-2xl border border-gray-300 text-gray-700 font-medium hover:bg-gray-100 transition"
                >
                    Cancel
                </button>


                <!-- Delete -->
                <button
                    @click="confirmDelete"
                    class="flex-1 py-3 rounded-2xl bg-(--color-delete-icon) text-white font-medium hover:opacity-90 transition"
                >  
                    Delete
                </button>

            </div>

        </div>

    </div>

</template>


<script setup>


// ==============================
// Props
// ==============================

const props = defineProps({

    expenseId: {
        type: Number,
        required: true
    }

});


// ==============================
// Emits
// ==============================

const emit = defineEmits([
    'close',
    'delete'
]);


// ==============================
// Confirm Delete
// ==============================

function confirmDelete() {

    emit('delete', props.expenseId);

}

</script>