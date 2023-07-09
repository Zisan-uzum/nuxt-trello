<script setup>

import {ref} from 'vue'

const newWorkspaceName = ref("")
const workspaceList = ref([
    { id: 1, name: "Test1" },
    {id:2, name: "Test2"}
])

const createNewWorkspace = () => {
    const randomId = Math.floor(Math.random() * 100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value
    })
}

</script>


<template>

<h1>Home Page</h1>
<h2>Recently viewed</h2>
<h2>Workspaces</h2>

<input type="text" v-model="newWorkspaceName"/>
<button @click="createNewWorkspace">Create a Workspace</button>
<ul>
    <li v-for="workspace in workspaceList" :key="`workspace+ ${workspace.id}`"> {{ workspace.id }}:  {{ workspace.name }}</li>
</ul>
</template>

<style>

</style>