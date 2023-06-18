<script setup>
import { Link } from '@inertiajs/vue3';
</script>

<template>
    <div class="h-[100vh] flex flex-col items-center pt-[100px] bg-gray-100 dark:bg-gray-900">
        <div>
            <Link :href="route('login')">
                <img width="200" src="/images/icons/FacebookLogo.png" alt="">
            </Link>
        </div>

        <div
            class="w-full px-6 py-4 mt-6 overflow-hidden bg-white shadow-md sm:max-w-md dark:bg-gray-800 sm:rounded-lg"
        >
            <slot />
        </div>
    </div>
</template>
