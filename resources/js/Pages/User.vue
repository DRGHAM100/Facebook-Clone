<script setup>
import { Link, Head } from '@inertiajs/vue3';
import MainNavLayout from '@/Layouts/MainNavLayout.vue';
import CreatePostBox from '@/Components/CreatePostBox.vue';
import Post from '@/Components/Post.vue';

import Camera from 'vue-material-design-icons/Camera.vue'
import Pen from 'vue-material-design-icons/Pen.vue'

import { useGeneralStore } from '@/Stores/general';
import { storeToRefs } from 'pinia';
const useGeneral = useGeneralStore()
const { isCropperModal, isImageDisplay } = storeToRefs(useGeneral)

defineProps({ posts: Object, user: Object })

</script>

<template>
    <Head title="Profile" />

    <MainNavLayout>
        <div class="w-full min-h-[100vh] pb-20 bg-[#F1F2F5]">
            <div class="w-full bg-white">
                <div class="max-w-[1100px] pt-[56px] mx-auto pb-1">
                    <img class="rounded-b-xl" src="https://picsum.photos/id/45/2000/320">

                    <div id="ProfileInfo" class="flex flex-col items-center justify-between px-4 md:flex-row">
                        <div class="flex flex-col items-center gap-4 -mt-16 md:flex-row md:-mt-6">
                            <div class="relative">
                                <img
                                    class="rounded-full w-[165px] h-[165px] border-white border-4"
                                    :src="user.image"
                                >
                                <button
                                    v-if="$page.props.auth.user.id === user.id"
                                    @click="isCropperModal = true"
                                    class="absolute right-0 top-[100px] bg-gray-200 hover:bg-gray-300 p-1.5 rounded-full cursor-pointer"
                                >
                                    <Camera :size="25"/>
                                </button>
                            </div>
                            <div class="-mt-3 text-center md:mt-4 md:text-left">
                                <div class="text-[28px] font-extrabold pt-1">
                                    {{ user.name }}
                                </div>
                                <div class="text-[17px] font-bold text-gray-600 mb-1.5 text-center md:text-left">234 friends</div>
                                <div class="flex justify-center md:justify-start md:-ml-1">
                                    <img
                                        class="rounded-full -ml-1 z-[10] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/141/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[9] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/142/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[8] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/143/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[7] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/144/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[6] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/145/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[5] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/146/2000/320"
                                    >
                                    <img
                                        class="rounded-full -ml-3 z-[4] w-[40px] h-[40px] border-white border-2"
                                        src="https://picsum.photos/id/147/2000/320"
                                    >
                                </div>
                            </div>
                        </div>

                        <Link
                            v-if="$page.props.auth.user.id === user.id"
                            :href="route('profile.edit')"
                            class="
                                flex
                                justify-center
                                w-7/12
                                md:w-[160px]
                                items-baseline
                                md:my-0
                                my-4
                                bg-gray-200
                                hover:bg-gray-300
                                rounded-lg
                                cursor-pointer
                            "
                        >
                            <button class="flex items-center px-5 py-2 font-bold">
                                <Pen class="mr-1 -ml-2" :size="22"/> Edit profile
                            </button>
                        </Link>
                    </div>

                    <div class="flex items-centerw-full border-t h-[50px] py-[4px]">
                        <button class="w-[85px]">
                            <div
                                class="
                                    flex
                                    items-center
                                    text-[15px]
                                    justify-center
                                    h-[45px]
                                    text-blue-500
                                    hover:bg-[#F2F2F2]
                                    w-full
                                    font-bold
                                    rounded-lg
                                    cursor-pointer
                                "
                            >
                                Posts
                            </div>
                            <div class="border-b-4 rounded-md border-b-blue-400"></div>
                        </button>
                        <button class="flex items-center text-[15px] justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-[85px] font-bold rounded-lg mx-1 cursor-pointer">
                            About
                        </button>
                        <button class="flex items-center text-[15px] justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-[85px] font-bold rounded-lg mx-1 cursor-pointer">
                            Friends
                        </button>
                        <button class="flex items-center text-[15px] justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-[85px] font-bold rounded-lg mx-1 cursor-pointer">
                            Videos
                        </button>
                        <button class="flex items-center text-[15px] justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-[85px] font-bold rounded-lg mx-1 cursor-pointer">
                            Photos
                        </button>
                        <button class="flex items-center text-[15px] justify-center h-[48px] p-1 hover:bg-[#F2F2F2] w-[85px] font-bold rounded-lg mx-1 cursor-pointer">
                            Check-ins
                        </button>
                    </div>
                </div>
            </div>

            <div class="flex-cols md:flex w-full max-w-[1100px] justify-between h-[calc(100%-56px)] md:px-0 px-2 mx-auto">

                <div id="LeftSection" class="w-full mt-4 mr-4 md:w-5/12">
                    <div class="p-3 bg-white rounded-lg shadow-lg">
                        <div class="pb-2 text-xl font-extrabold">Intro</div>
                        <div class="pb-5">
                            <button class="w-full p-2 font-bold bg-gray-200 rounded-lg hover:bg-gray-300">
                                Add bio
                            </button>
                        </div>
                        <div class="pb-5">
                            <button class="w-full p-2 font-bold bg-gray-200 rounded-lg hover:bg-gray-300">
                                Edit details
                            </button>
                        </div>
                        <div class="pb-5">
                            <button class="w-full p-2 font-bold bg-gray-200 rounded-lg hover:bg-gray-300">
                                Add hobbies
                            </button>
                        </div>
                        <div>
                            <button class="w-full p-2 font-bold bg-gray-200 rounded-lg hover:bg-gray-300">
                                Add feature
                            </button>
                        </div>
                    </div>

                    <div class="p-3 mt-4 bg-white rounded-lg shadow-lg">
                        <div class="pb-2 text-xl font-extrabold">Photos</div>
                        <div class="flex flex-wrap items-center justify-start w-full">
                            <span
                                v-for="photo in posts.data"
                                :key="photo"
                                class="w-1/3"
                                v-show="photo.image !== null"
                            >
                                <img
                                    @click="isImageDisplay = photo.image"
                                    class="object-cover p-1 rounded-lg cursor-pointer aspect-square"
                                    :src="photo.image"
                                >
                            </span>
                        </div>
                    </div>
                </div>

                <div id="PostsSection" class="w-full overflow-auto md:w-7/12">

                    <CreatePostBox
                        v-if="$page.props.auth.user.id === user.id"
                        :image="user.image"
                        :placeholder="'What\'s on your mind ' + user.name "
                    />

                    <div v-for="post in posts.data" :key="post">
                        <Post :user="post.user" :post="post" :comments="post.comments" />
                    </div>

                </div>

            </div>
        </div>
    </MainNavLayout>
</template>
