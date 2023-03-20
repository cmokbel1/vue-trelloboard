<script setup lang="ts">
import type { Column } from "../types";
import { nanoid } from "nanoid";

const columns = ref<Column[]>([
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                id: nanoid(),
                title: "Create landing page",
                createdAt: new Date()
            }
        ],
    },
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                id: nanoid(),
                title: "Create landing page",
                createdAt: new Date()
            }
        ],
    },
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                id: nanoid(),
                title: "Create landing page",
                createdAt: new Date()
            }
        ],
    },
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                id: nanoid(),
                title: "Create landing page",
                createdAt: new Date()
            }
        ],
    }
])

</script>
<template>
    <div class="flex gap-4 overflow-x-auto items-start">
        <div v-for="column in columns" :key="column.id"
        class="bg-gray-200 p-5 rounded min-w-[250px]"
        >
        <header class="font-bold mb-4">
                {{ column.title }}
        </header>
        <TrelloBoardTask v-for="task in column.tasks" :task="task" />
        <footer>
            <button class="text-gray-500">+ Add Card</button>
        </footer>    
    </div>
</div>
</template>