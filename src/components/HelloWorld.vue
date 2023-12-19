<script setup lang="ts" xmlns="http://www.w3.org/1999/html">
import {ref} from 'vue'
import axios from "axios";

defineProps<{ msg: string }>()

const server = ref("")
const axiosOrFetch = ref("axios")
const send = (link: string, body?: any | undefined): boolean => {
    if (axiosOrFetch.value === "axios") { // It is axios method
        axios.post(server.value + link, body)
            .then((response) => {
                console.log(response)
            })
            .catch(err => {
                console.error(err)
            })
    } else {
        fetch(server.value + link, {
            method: "POST",
            body,
        })
            .then(res => res.json())
            .then(json => console.log(json))
            .catch(err => {
                console.error(err)
            })
    }
    return true
}
</script>

<template>
    <h1>{{ msg }}</h1>
    <span>All the things will print in the console</span>
    <span>所有的返回信息都会呈现在控制台中</span><br>
    <span>link and code never changes</span>
    <span>查询码和访问码永远不会改变:</span><br>
    <span>Link:MIROLLSDEVELOPERTOLLS Code:DEVELOPERTOLLSMIROLLS</span>
    <div>Axios<input v-model="axiosOrFetch" type="radio" value="axios"></div>
    <div>Fetch<input v-model="axiosOrFetch" type="radio" value="fetch"></div>
    <div>
        <input type="text" placeholder="Server Domain/IP" v-model="server">
    </div>
    <p>Normal</p>
    <div>Get site
        <button type="button" @click='send("/get/site")'>Send</button>
    </div>
    <div>Answer questionnaire
        <button type="button"
                @click='send("/answer",{link: "MIROLLSDEVELOPERTOLLS",answer: [{title: "问题标题",type: "radio",answer: [false,false,false]},{title:"问题题目",answer:["yep"],type:"blank"}]})'>
            Send
        </button>
    </div>
    <div>Create questionnaire
        <button type="button" @click='send("/roll/create",{title:"问卷标题", quest:[{type:"radio", optionsNumber:3, 选择题特有的选项title:"问题题目",options: ["选项1","选项2","选项3"]},{type:"blank",placeholder:"题目的提示",title:"问题的题目"}],})'>Send</button>
    </div>
    <div>Get Rolls

    </div>
</template>

<style scoped>
</style>
