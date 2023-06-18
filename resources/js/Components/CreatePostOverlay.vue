<script setup>
import { ref, reactive } from 'vue'
import { router, usePage } from '@inertiajs/vue3';

import VideoImage from 'vue-material-design-icons/VideoImage.vue'
import Image from 'vue-material-design-icons/Image.vue'
import EmoticonOutline from 'vue-material-design-icons/EmoticonOutline.vue'
import Close from 'vue-material-design-icons/Close.vue'
import ChevronDown from 'vue-material-design-icons/ChevronDown.vue'
import Earth from 'vue-material-design-icons/Earth.vue'
import DotsHorizontal from 'vue-material-design-icons/DotsHorizontal.vue'

import { useGeneralStore } from '@/Stores/general';
import { storeToRefs } from 'pinia';
const useGeneral = useGeneralStore()
const { isPostOverlay } = storeToRefs(useGeneral)

const emit = defineEmits(['showModal'])

const user = usePage().props.auth.user

let imageDisplay = ref('')

const form = reactive({
    text: null,
    image: null,
})
let error = ref(null)

const createPost = () => {
    router.post('/post', form, {
        forceFormData: true,
        preserveScroll: true,
        onError: errors => {
            errors && errors.text ? error.value = errors.text : ''
            errors && errors.image ? error.value = errors.image : ''
        },
        onSuccess: () => {
            form.text = null
            form.image = null
            imageDisplay.value = null
            emit('showModal', false)
        }
    })
}

const getUploadedImage = (e) => {
    imageDisplay.value = URL.createObjectURL(e.target.files[0])
    form.image = e.target.files[0]
}

const clearImage = () => {
    imageDisplay.value = null
    form.image = null
}
</script>

<template>
    <div id="CreatePostOverlay" class="fixed top-0 left-0 z-50 w-full h-full bg-white bg-opacity-70">
        <div class="grid h-screen p-4 place-items-center">
            <div class="bg-white w-full max-w-[600px] mx-auto shadow-xl rounded-xl">
                <div class="flex items-center relative my-3.5 mx-1">
                    <div class="text-[22px] font-extrabold w-full text-center">
                        Create Post
                    </div>
                    <div
                        @click="isPostOverlay = false"
                        class="absolute right-3 rounded-full p-1.5 bg-gray-200 hover:bg-gray-300 cursor-pointer"
                    >
                        <Close :size="28" fillColor="#5E6771"/>
                    </div>
                </div>

                <div class="border-t border-t-gray-300">
                    <div class="p-4">


                        <div class="flex items-center">
                            <img class="rounded-full ml-1 min-w-[45px] max-h-[45px]" :src="user.image">
                            <div class="ml-4">
                                <div class="font-extrabold">{{ user.name }}</div>
                                <div class="flex items-center justify-between w-[100px] bg-gray-200 p-0.5 px-2 rounded-lg">
                                    <Earth :size="18"/>
                                    <span class="font-bold pl-1.5 text-[13px]">Public</span>
                                    <ChevronDown class="pl-1 pr-10" :size="18"/>
                                </div>
                            </div>
                        </div>

                        <div class="max-h-[350px] overflow-auto">
                            <textarea
                                v-model="form.text"
                                class="w-full border-0 mt-4 focus:ring-0 text-[22px]"
                                placeholder="What's on your mind?"
                                cols="30"
                                rows="3"
                            ></textarea>
                            <div v-if="form.image" class="relative p-2 border border-gray-300 rounded-lg">
                                <Close
                                    @click="clearImage()"
                                    class="absolute bg-white p-0.5 m-2 right-2 rounded-full border cursor-pointer"
                                    :size="24"
                                    fillColor="#5E6771"
                                />
                                <img class="mx-auto rounded-lg" :src="imageDisplay">
                            </div>
                        </div>

                        <div class="flex items-center justify-between mt-4 border-2 shadow-sm rounded-xl">
                            <div class="p-4 font-extrabold">
                                Add to your post
                            </div>
                            <div class="flex items-center">

                                <label
                                    for="image"
                                    class="p-2 rounded-full cursor-pointer hover:bg-gray-200"
                                >
                                    <Image :size="27" fillColor="#43BE62"/>
                                </label>
                                <input
                                    id="image"
                                    class="hidden"
                                    type="file"
                                    @input="getUploadedImage($event)"
                                >

                                <button class="p-2 rounded-full cursor-pointer hover:bg-gray-200">
                                    <EmoticonOutline :size="27" fillColor="#F8B927"/>
                                </button>
                                <button class="p-2 rounded-full cursor-pointer hover:bg-gray-200">
                                    <VideoImage :size="27" fillColor="#F12848"/>
                                </button>
                                <button class="p-2 rounded-full cursor-pointer hover:bg-gray-200">
                                    <DotsHorizontal :size="27" fillColor="#050505"/>
                                </button>
                            </div>
                        </div>

                        <div v-if="error">
                            <div class="w-full mt-3 text-center text-red-700 bg-red-100 rounded-lg">
                                <div class="p-0.5">
                                    {{ error }}
                                </div>
                            </div>
                        </div>

                        <button
                            @click="createPost"
                            class="w-full bg-blue-500 hover:bg-blue-600 text-white font-extrabold p-1.5 mt-3 rounded-lg"
                        >
                            Post
                        </button>

                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
