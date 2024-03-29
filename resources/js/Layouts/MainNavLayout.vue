<script setup>
import { ref } from 'vue';
import Magnify from 'vue-material-design-icons/Magnify.vue'
import Home from 'vue-material-design-icons/Home.vue'
import HomeOutline from 'vue-material-design-icons/HomeOutline.vue'
import TelevisionPlay from 'vue-material-design-icons/TelevisionPlay.vue'
import StoreFrontOutline from 'vue-material-design-icons/StoreFrontOutline.vue'
import AccountGroup from 'vue-material-design-icons/AccountGroup.vue'
import COntrollerClassicOutline from 'vue-material-design-icons/COntrollerClassicOutline.vue'
import DotsGrid from 'vue-material-design-icons/DotsGrid.vue'
import FacebookMessenger from 'vue-material-design-icons/FacebookMessenger.vue'
import Bell from 'vue-material-design-icons/Bell.vue'
import Logout from 'vue-material-design-icons/Logout.vue'

import CropperModal from '@/Components/CropperModal.vue';
import ImageDisplay from '@/Components/ImageDisplay.vue';
import CreatePostOverlay from '@/Components/CreatePostOverlay.vue';

import { useGeneralStore } from '@/Stores/general';
import { storeToRefs } from 'pinia';
import { usePage } from '@inertiajs/vue3';
const useGeneral = useGeneralStore();
const { isPostOverlay, isCropperModal, isImageDisplay } = storeToRefs(useGeneral);

const user = usePage().props.auth.user;
let showMenu = ref(false);
</script>

<template>
    <div id="MainNav"
        class="fixed z-50 w-full flex items-center justify-between h-[56px] bg-white shadow-xl border-b"
    >
        <div class="flex items-center justify-start w-[260px]">
            <Link href="/" class="pl-3 min-w-[55px]">
                <img
                class="w-[40px]"
                src="/images/icons/FacebookLogoCircle.png" alt="">
            </Link>
            <div class="flex items-center justify-center bg-[#EFF2F5] p-1 rounded-full h-[40px] ml-2">
                <Magnify class="p-1" :size="22" fillColor="#646768"/>
                <input
                    class="lg:block hidden border-none p-0 bg-[#EFF2F5] placeholder-[#646768] ring-0 focus:ring-0"
                    placeholder="Search Facebook"
                type="text">
            </div>
        </div>

        <div id="NavCenter" class="hidden lg:flex items-center ml-5 justify-center w-8/12 max-w-[600px]">
            <Link href="/" class="w-full">
                <div
                :class="$page.url === '/' ? 'mt-1.5' : ''"
                class="flex items-center justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-full rounded-lg cursor-pointer
                ">
                    <div>
                        <Home v-if="$page.url === '/'" class="mx-auto" :size="27" fillColor="#1A73E3"/>
                        <HomeOutline v-else class="mx-auto" :size="32" fillColor="#646768"/>
                    </div>
                </div>
                <div
                    v-if="$page.url === '/'"
                    class="border-b-4 rounded-md border-b-blue-400"
                >
                </div>
            </Link>
            <button class="flex items-center justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-full rounded-lg mx-1 cursor-pointer">
                <TelevisionPlay class="mx-auto" :size="27" fillColor="#646768"/>
            </button>
            <button class="flex items-center justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-full rounded-lg mx-1 cursor-pointer">
                <StoreFrontOutline class="mx-auto" :size="27" fillColor="#646768"/>
            </button>
            <button class="flex items-center justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-full rounded-lg mx-1 cursor-pointer">
                <span class="rounded-full border-[2px] border-[#646768] p-1">
                    <AccountGroup class="mx-auto" :size="22" fillColor="#646768"/>
                </span>
            </button>
            <button class="flex items-center justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-full rounded-lg mx-1 cursor-pointer">
                <COntrollerClassicOutline class="mx-auto" :size="32" fillColor="#646768"/>
            </button>
        </div>
        <div class="flex items-center justify-end w-2/12 mr-4">
            <button class="rounded-full bg-[#E3E6EA] p-2 hover:bg-gray-300 mx-1 cursor-pointer">
                <DotsGrid :size="23" fillColor="#050505"/>
            </button>
            <button class="rounded-full bg-[#E3E6EA] p-2 hover:bg-gray-300 mx-1 cursor-pointer">
                <FacebookMessenger :size="23" fillColor="#050505"/>
            </button>
            <button class="rounded-full bg-[#E3E6EA] p-2 hover:bg-gray-300 mx-1 cursor-pointer">
                <Bell :size="23" fillColor="#050505"/>
            </button>
            <div class="relative flex items-center justify-center">
                <button @click="showMenu = !showMenu">
                    <img class="rounded-full ml-1 min-w-[40px] max-h-[40px] cursor-pointer"
                    :src="user.image"
                    >
                </button>
                <div v-if="showMenu" class="absolute bg-white shadow-xl top-10 right-0 w-[330px] rounded-lg p-1 border mt-1">
                    <Link :href="route('user.show', { id: user.id })" @click="showMenu = !showMenu">
                        <div class="flex items-center gap-3 p-2 rounded-lg hover:bg-gray-200">
                            <img class="rounded-full ml-1 min-w-[35px] max-h-[35px] cursor-pointer"
                                :src="user.image"
                            >
                            <span>{{ user.name }}</span>
                        </div>
                    </Link>
                    <Link
                    class="w-full"
                    :href="route('logout')"
                    as="button"
                    method="post"
                    >
                        <div class="flex items-center gap-3 hover:bg-gray-200 px-2 py-2.5 rounded-lg">
                            <Logout class="pl-2" :size="30"/>
                            <span>Logout</span>
                        </div>
                    </Link>
                    <div class="p-2 pt-3 mt-1 text-xs font-semibold border-t">
                        Privacy . Terms . Advertising © 2023
                    </div>
                </div>
            </div>
        </div>
    </div>



    <slot/>

    <CreatePostOverlay
        v-if="isPostOverlay"
        @showModal="isPostOverlay = false"
    />

    <CropperModal
        v-if="isCropperModal"
        @showModal="isCropperModal = false"
    />

    <ImageDisplay
        v-if="isImageDisplay != null"
    />
</template>
