            <script setup>
            import { ref, onMounted } from 'vue'
            import { ArrowLeftCircleIcon, ArrowRightCircleIcon } from '@heroicons/vue/24/solid'

            const users = ref([])

            onMounted(async () => {
                const res = await fetch('/src/users.json')
                users.value = await res.json()
            })

            const slider = ref(null)

            const scrollLeft = () => {
                slider.value.scrollLeft -= 300
            }

            const scrollRight = () => {
                slider.value.scrollLeft += 300
            }



</script>

<template>
    <div class="relative w-full overflow-hidden bg-gradient-to-br from-blue-500 to-blue-700 py-10">
        <div class="flex items-center justify-between px-5 mb-4">
            <button @click="scrollLeft"
                class="w-10 h-10 bg-white rounded-full flex items-center justify-center shadow-lg text-blue-700">
                <ArrowLeftCircleIcon class="w-6 h-6 text-blue-500 cursor-pointer" />
            </button>
            <button @click="scrollRight"
                class="w-10 h-10 bg-white rounded-full flex items-center justify-center shadow-lg text-blue-700 ">
                <ArrowRightCircleIcon class="w-6 h-6 text-blue-500 cursor-pointer" />
            </button>
        </div>

        <div ref="slider" class="flex gap-4 space-x-6 overflow-x-auto scrollbar-hide px-5 transition-all duration-300">
            <div v-for="user in users" :key="user.id"
                class="min-w-[250px] bg-white rounded-xl shadow-lg p-5 flex flex-col items-center">
                <img :src="user.image" alt="avatar" class="w-30 h-30 rounded-full border-4 border-blue-500 mb-3" />
                <h2 class="text-xl font-semibold">{{ user.name }}</h2>
                <p class="text-sm text-gray-500">{{ user.role }}</p>
            </div>
        </div>
    </div>
</template>


<style>
.scrollbar-hide::-webkit-scrollbar {
    display: none;
}
</style>