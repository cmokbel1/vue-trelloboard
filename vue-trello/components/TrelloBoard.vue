<script setup lang="ts">
import type { Column, Task } from "../types";
import { nanoid } from "nanoid";
import draggable from "vuedraggable";

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
        title: "newLog",
        tasks: [
            {
                id: nanoid(),
                title: "Create landing page",
                createdAt: new Date()
            }
        ],
    }
])
const alt = useKeyModifier("Alt");

</script>
<template>
    <div>
        <draggable 
        v-model="columns"
        group="columns"
        item-key="id"
        class="flex gap-4 overflow-x-auto items-start"
        :animation="150"
        handle=".drag-handle">
            <template #item="{ element: column }: {element: Column}">
                <div class="bg-gray-200 p-5 rounded min-w-[250px]">
                    <header class="font-bold mb-4">
                        <DragHandle />
                        {{ column.title }}
                    </header>
                    <draggable 
                    v-model="column.tasks"
                    :group="{name: 'tasks', pull: alt ? 'clone' : true }"
                    item-key="id"
                    :animation="150"
                    handle=".drag-handle">
                        <template #item="{element: task}: {element: Task}">
                            <div>
                            <TrelloBoardTask :task="task" />
                            </div>
                        </template>
                    </draggable>
                    <footer>
                        <NewTask @add="column.tasks.push($event)"/>    
                    </footer>
                </div>
            </template>
        </draggable>
    </div>
</template>