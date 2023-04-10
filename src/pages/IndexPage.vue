<template>
  <q-page padding class="flex">
    <KanbanBoard :columns="data.columns"></KanbanBoard>
  </q-page>
</template>

<script setup>
import KanbanBoard from "src/components/KanbanBoard.vue";
import kanban from "src/components/kanban.json";
import { ref } from "vue";

const data = ref(kanban);
</script>
