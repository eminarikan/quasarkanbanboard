<template>
  <q-page class="flex justify-center">
    <div class="b"></div>
    <KanbanBoard :columns="data.columns"></KanbanBoard>
  </q-page>
</template>

<script setup>
import KanbanBoard from "src/components/KanbanBoard.vue";
import kanban from "src/components/kanban.json";
import { ref } from "vue";
// #81b1a8
const data = ref(kanban);
</script>
<style scoped>
.b {
  background-color: #1b73b8;
  background: linear-gradient(
    90deg,
    rgba(27, 115, 184, 1) 0%,
    rgba(129, 177, 168, 1) 100%
  );
  min-height: 20%;
  min-width: 100vw;
  position: absolute;
  z-index: -1;
}
</style>
