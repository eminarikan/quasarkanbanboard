<template>
  <q-card flat class="row justify-center q-gutter-sm full-width">
    <div v-for="(column, key) in columns" :key="key">
      <draggable
        class="b"
        v-model="column.list"
        group="todos"
        @start="drag = true"
        @end="drag = false"
        item-key="id"
      >
        <template #header>
          <q-bar
            :class="`bg-${column.color} text-white row justify-between list-header`"
          >
            <div class="text-h6">
              {{ column.list.length + " " + column.label }}
            </div>
            <q-btn flat round dense icon="more_vert" />
          </q-bar>
        </template>
        <template #item="{ element }">
          <q-card class="q-pa-sm q-mt-sm item-card" style="cursor: move">
            <q-card-section class="flex justify-between">
              <div>{{ element.id }}</div>
              <q-chip icon="person" :label="element.name" />
            </q-card-section>
            <q-card-section class="flex justify-between">
              <div>{{ element.description }}</div>
            </q-card-section>
          </q-card>
        </template>
      </draggable>
    </div>
  </q-card>
</template>

<script setup>
import draggable from "vuedraggable";
import { ref, defineProps } from "vue";

const props = defineProps({
  columns: Array,
});

const drag = ref(false);
</script>

<style scoped>
.b {
  border: 1px solid black;
}
.list-header {
  background: #000;
  border-top-right-radius: 0.3rem;
  border-top-left-radius: 0.3rem;
}
.item-card:hover {
  background-color: antiquewhite;
}
</style>
