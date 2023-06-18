<script setup>
import { onMounted, ref } from 'vue';

defineProps(['modelValue', 'placeholder']);

defineEmits(['update:modelValue']);

const input = ref(null);

onMounted(() => {
    if (input.value.hasAttribute('autofocus')) {
        input.value.focus();
    }
});

defineExpose({ focus: () => input.value.focus() });
</script>

<template>
    <input
        class="p-4 text-lg font-semibold border-gray-300 rounded-md shadow-sm focus:border-indigo-300 focus:ring-indigo-300"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        ref="input"
        :placeholder="placeholder"
    />
</template>
