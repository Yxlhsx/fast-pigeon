<script setup lang="ts">
import { onMounted, watch, ref } from 'vue'
import log from '../../utils/log'

const props = defineProps<{ modelValue: string; focusd: boolean }>()

const emit = defineEmits<{
    (event: 'submit-search'): void
    (event: 'update:modelValue', value: string): void
    (event: 'update:focusd', focusd: boolean): void
}>()

const searchInputELe = ref<HTMLElement | null>()

watch(
    () => props.modelValue,
    v => {
        emit('update:modelValue', v)
    }
)

onMounted(() => {
    log.info('测试输出日志')
    if (props.focusd) {
        searchInputELe.value && searchInputELe.value.focus()
    }
})

function submit() {
    emit('submit-search')
}

function handleFocus(e: Event) {
    emit('update:focusd', true)
}

function handleBlur(e: Event) {
    emit('update:focusd', false)
}
</script>

<template>
    <div class="primary-search-input">
        <img v-show="focusd" src="https://files.codelife.cc/itab/search/baidu.svg" alt="百度" />
        <input
            id="search"
            v-model="modelValue"
            type="text"
            ref="searchInputELe"
            @keyup.enter="submit"
            @focus="handleFocus"
            @blur="handleBlur"
        />
    </div>
</template>

<style>
.primary-search-input {
    display: flex;
    align-items: center;
    padding: 0 10px;
    width: 400px;
    height: 50px;
    background-color: rgba(143, 143, 143, 0.3);
    border-radius: 16px;
    transition: all 0.4s;
}

.primary-search-input > input {
    padding: 0 10px;
    width: 100%;
    height: 100%;
    outline: none;
    border: none;
    font-size: 16px;
    background-color: transparent;
}

.primary-search-input:focus-within {
    width: 600px;
    transform: scale(1.1);
    background-color: rgba(143, 143, 143, 0.9);
}
</style>
