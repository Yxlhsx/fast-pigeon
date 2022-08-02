<script setup lang="ts">
import { ref } from 'vue'
import PrimarySearchInputVue from '@/components/PrimarySearchInput/PrimarySearchInput.vue'

const keyWord = ref('')

const focusd = ref(true)

function submitSearch() {
    window.location.href = `https://www.baidu.com/s?ie=UTF-8&wd=${keyWord.value}`
}
</script>

<template>
    <main>
        <primary-search-input-vue
            v-model="keyWord"
            v-model:focusd="focusd"
            @submit-search="submitSearch"
        />
    </main>
</template>

<style scoped>
main {
    width: 100vw;
    height: 100vh;
    overflow: auto;
    background-image: url('https://w.wallhaven.cc/full/6o/wallhaven-6ozkzl.jpg');
}

.primary-search-input {
    margin: 10% auto;
}
</style>
