<script>
import { workspaceList } from "../../store/global.js"
export default {

    setup() {
        console.log(workspaceList.value)
        return {
            workspaceList
        }
    },

    data: () => ({
        workspaceName: "",
        newColumName: "",
        boards: [

        ]
    }),

    methods: {
        createNewColumn() {
            if (this.newColumName.length > 0) {
                this.boards.push({
                    name: this.newColumName,
                    items: [],
                    newItemName: ""
                })
            }
            this.newColumName = ""
        },
        createNewCard(board) {
            if (board.newItemName.length > 0) {
                board.items.push({
                    id: Math.floor(Math.round() * 100),
                    name: board.newItemName,
                    explanation: "Explanation"
                })
                board.newItemName = ""
            }

        },
        changeColumn(item, board, column) {
            if (this.boards.includes(column)) {
                column.items.push(item);
                board.items = board.items.filter((compare) => compare !== item)
            }
        }

    },
    mounted() {

        this.workspaceName = this.workspaceList.find((workspace) => workspace.id === Number(this.$route.params.id)).name
        console.log(typeof (this.$route.params.id))
    }

}
</script>

<template>
    <h1>{{ workspaceName }} Workspace (#{{ this.$route.params.id }}) </h1>
    <section>
        <input type="text" placeholder="New Column Title" @keyup.enter="createNewColumn" v-model="newColumName" />
        <button @click="createNewColumn">Create Column</button>
    </section>

    <div class="flex flex-row justify-center items-center">
        <section v-for="board in boards">
            <div class="card bg-base-300 text-secondary">
                <div class="card-body">

                    <h2 class="card-title">{{ board.name }}</h2>

                    <div class="flex flex-row">
                        <input type="text" placeholder="New Card Title" @keyup.enter="createNewCard(board)"
                            v-model="board.newItemName" />
                        <button class="bg-white" @click="createNewCard(board)">Create Card</button>
                    </div>

                    <div v-for="item in board.items" class="bg-accent-focus">
                        <h3>Name is {{ item.name }}</h3>
                        <p class="w-full overflow-hidden ">Situation of it{{ item.explanation }}</p>
                        <div className="dropdown dropdown-end">
                            <label tabIndex={0} className="btn m-1">Situation</label>
                            <ul tabIndex={0}
                                className="dropdown-content z-[1] menu p-2 shadow bg-base-100 rounded-box w-52">
                                <li class="cursor-pointer" v-for="column in boards"
                                    @click="changeColumn(item, board, column)">{{
                                        column.name }}
                                </li>
                            </ul>
                        </div>
                    </div>

                </div>
            </div>
        </section>
    </div>
</template>

<style></style>