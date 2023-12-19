<script setup lang="ts">
import {ref} from 'vue'

defineProps<{ msg: string }>()

const server = ref("")
const axios = ref("axios")
const send = (link: string, body: any): boolean => {
    return true
}
</script>

<template>
    <h1>{{ msg }}</h1>
    <span>All the things will print in the console</span>
    <span>所有的返回信息都会呈现在控制台中</span>
    <div>Axios<input v-model="axios" type="radio" value="axios"></div>
    <div>Fetch<input v-model="axios" type="radio" value="fetch"></div>
    <div>
        <input type="text" placeholder="Server Domain/IP" v-model="server">
    </div>
    <button type="button" @click="send">Send</button>
</template>

<style scoped>
</style>
