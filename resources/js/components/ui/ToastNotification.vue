<script setup>
import { useToasterStore } from '../../store/Toast';
const toastStore = useToasterStore()
const statusClasses = {
  success: "text-green-500 bg-green-100",
  error: "text-red-500 bg-red-100",
  warning: "text-orange-500 bg-orange-100",
};
</script>

<template>
  <Teleport to="body">
    <div class="fixed top-5 right-5 space-y-2 z-50">
      <div
        v-for="toast in toastStore.toasts"
        :key="toast.id"
        class="flex items-center w-full max-w-xs p-4 text-gray-100 bg-secondary rounded-lg shadow-lg"
        role="alert"
      >
        <div
          class="inline-flex items-center justify-center shrink-0 w-8 h-8 rounded-lg"
          :class="statusClasses[toast.status]"
        >
          <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
            <path
              v-if="toast.status === 'success'"
              d="M10 .5a9.5 9.5 0 1 0 9.5 9.5A9.51 9.51 0 0 0 10 .5Zm3.707 8.207-4 4a1 1 0 0 1-1.414 0l-2-2a1 1 0 0 1 1.414-1.414L9 10.586l3.293-3.293a1 1 0 0 1 1.414 1.414Z"
            />
            <path
              v-else-if="toast.status === 'error'"
              d="M10 .5a9.5 9.5 0 1 0 9.5 9.5A9.51 9.51 0 0 0 10 .5Zm3.707 11.793a1 1 0 1 1-1.414 1.414L10 11.414l-2.293 2.293a1 1 0 0 1-1.414-1.414L8.586 10 6.293 7.707a1 1 0 0 1 1.414-1.414L10 8.586l2.293-2.293a1 1 0 0 1 1.414 1.414L11.414 10l2.293 2.293Z"
            />
            <path
              v-else
              d="M10 .5a9.5 9.5 0 1 0 9.5 9.5A9.51 9.51 0 0 0 10 .5ZM10 15a1 1 0 1 1 0-2 1 1 0 0 1 0 2Zm1-4a1 1 0 0 1-2 0V6a1 1 0 0 1 2 0v5Z"
            />
          </svg>
        </div>
        <div class="ms-3 text-sm font-normal">{{ toast.text }}</div>
        <button
          type="button"
          class="ms-auto p-1.5 rounded-lg focus:ring-2 focus:ring-gray-300 text-gray-100 hover:text-gray-900 hover:bg-gray-100"
          @click="toastStore.toasts = toastStore.toasts.filter(t => t.id !== toast.id)"
          aria-label="Close"
        >
          <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
          </svg>
        </button>
      </div>
    </div>
  </Teleport>
</template>
