<script setup lang="ts">
import { Task } from "@/types";
import { nanoid } from "nanoid";

const emit=defineEmits<{
    (e:"add", payload: Task):void;
}>()

const focused = ref(false);
const title = ref("");

function createTask(e: Event) {

    if (title.value.trim()) {
        e.preventDefault();
        emit("add", {
            title: title.value.trim(),
            createdAt: new Date(),
            id: nanoid()
        } as Task);
    }
    title.value = "";
}
</script>
<template>
<div>
    <textarea
    v-model="title"
    @keydown.tab="createTask"
    @keyup.enter="createTask"
    class="focus:bg-white focus:shadow resize-none rounded w-full border-none p-2 flex bg-transparent"
    :class ="{
        'h-7': !focused,
        'h-20': focused,
    }"
    style="outline: none !important"
    @focus="focused = true"
    @blur="focused = false"
    :placeholder="focused ? 'Enter a task title..' : '+ Add Card' ">
    </textarea>
</div>
</template>
<style>

</style>