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

function createColumn() {
    const column: Column = {
        id: nanoid(),
        title: "New Column",
        tasks: []
    };
    columns.value.push(column);
    // nextTick(() => {
    //     (document.querySelector(
    //         ".column:last-of-type .title-input"
    //      ) as HTMLInputElement).focus();
    // });
}
</script>
<template>
    <div class="flex items-start overflow-x-auto gap-4">
        <draggable 
        v-model="columns" 
        group="columns" 
        item-key="id" 
        class="flex gap-4 items-start" 
        :animation="150"
        handle=".drag-handle">
            <template #item="{ element: column }: { element: Column }">
                <div class="bg-gray-200 p-5 rounded min-w-[250px]" tabindex="0">
                    <header class="font-bold mb-4 flex justify-between">
                        <div>
                            <DragHandle />
                            <input class="title-input bg-transparent focus:bg-white rounded px-1 w-4/5"
                                @keyup.enter="($event.target as HTMLInputElement).blur()" 
                                type="text"
                                v-model="column.title" />
                        </div>
                        <CloseButton 
                        @click.prevent="columns = columns.filter((col) => col.id !== column.id)" 
                        />
                    </header>
                    <draggable 
                    v-model="column.tasks" 
                    :group="{ name: 'tasks', pull: alt ? 'clone' : true }" 
                    item-key="id"
                    :animation="150" handle=".drag-handle">
                        <template #item="{ element: task }: { element: Task }" class="flex">
                            <div>
                                <TrelloBoardTask :task="task" :column="column"
                                    @delete="column.tasks = column.tasks.filter((t) => t.id !== $event)" />
                            </div>
                        </template>
                    </draggable>
                    <footer>
                        <NewTask @add="column.tasks.push($event)" />
                    </footer>
                </div>
            </template>
        </draggable>
        <button @click="createColumn" class="bg-gray-200 whitespace-nowrap p-2 rounded opacity-50">
            +Create New Column
        </button>
    </div>
</template>