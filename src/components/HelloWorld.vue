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
    <h3>Normal</h3>
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
        <button type="button"
                @click='send("/roll/create",{title:"问卷标题", quest:[{type:"radio", optionsNumber:3,title:"问题题目",options: ["选项1","选项2","选项3"]},{type:"blank",placeholder:"题目的提示",title:"问题的题目"}],})'>
            Send
        </button>

    </div>
    <div>Get questionnaire
        <button type="button" @click='send("/get/roll",{link:"MIROLLSDEVELOPERTOLLS"})'>Send</button>
    </div>
    <div>Get Data Analysis
        <button type="button" @click='send("/query/roll",{code:"DEVELOPERTOLLSMIROLLS"})'>Send</button>
    </div>
    <h3>Install</h3>
    <div>Download
        <button type="button" @click='send("/install/download",{file:"default"})'>Send</button>
    </div>
    <div>Database (username: devtoolmrms; password:mrsdevtool, localhost, 3306, dbname:mirolls)
        <button type="button" @click='send("/install/set/database",{Username:"devtoolmrms",Password:"mrsdevtool",Protocol:"tcp",Host:"localhost",Port:3306,Database:"mirolls"})'>Send</button>
    </div>
    <div>Set Site
<!--        <button type="button" @click='send("/install/set/site",{Name})'>Send</button>-->
    </div>
</template>

<style scoped>
</style>
