<script setup>

import { ref } from 'vue'
import { workspaceList } from "../store/global.js"

definePageMeta({
    layout: "default",
});

const newWorkspaceName = ref("")
const test = useState('sfasdf', () => 4)

const createNewWorkspace = () => {
    const randomId = Math.floor(Math.random() * 100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value
    })

    newWorkspaceName.value = ""
}

</script>


<template>
    <h1>Home Page</h1>
    <h2>Recently viewed</h2>
    <h2>Workspaces</h2>

    <input type="text" v-model="newWorkspaceName" @keyup.enter="createNewWorkspace" />
    <button @click="createNewWorkspace">Create a Workspace</button>
    <ul>
        <li v-for="workspace in workspaceList" :key="`workspace+ ${workspace.id}`"> <nuxt-link
                :to="`/workspaces/${workspace.id}`"> {{ workspace.id }}: {{ workspace.name }} </nuxt-link></li>
    </ul>
</template>

<style></style>