<template>
  <q-card flat>
    <q-card-actions align="right">
      <q-btn color="primary" icon="add" label="Yeni" />
    </q-card-actions>
    <q-card-section class="row justify-center q-gutter-sm full-width">
      <div v-for="(column, key) in columns" :key="key">
        <draggable
          class="list-group"
          v-model="column.list"
          v-bind="dragOptions"
          group="todos"
          @start="drag = true"
          @end="drag = false"
        >
          <template #header>
            <q-bar
              :class="`bg-${column.color} text-white row justify-between list-header`"
            >
              <div class="text-h6">
                {{ column.list.length + " " + column.label }}
              </div>
              <q-btn-dropdown flat round dense dropdown-icon="more_vert">
                <q-list>
                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section avatar>
                      <q-icon name="edit" />
                    </q-item-section>
                    <q-item-section>
                      <q-item-label>Etiketi Değiştir</q-item-label>
                    </q-item-section>
                  </q-item>
                  <q-item clickable v-close-popup @click="onItemClick">
                    <q-item-section avatar>
                      <q-icon name="add" />
                    </q-item-section>
                    <q-item-section>
                      <q-item-label>Sütun Ekle/Çıkar</q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>
              </q-btn-dropdown>
            </q-bar>
          </template>
          <template #item="{ element }">
            <q-card flat bordered class="q-pa-sm q-mt-sm" style="cursor: move">
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
    </q-card-section>
  </q-card>
</template>

<script setup>
import draggable from "vuedraggable";
import { ref, defineProps, computed } from "vue";

const props = defineProps({
  columns: Array,
});

const drag = ref(false);

const dragOptions = computed(() => {
  return {
    animation: 300,
    group: "description",
    disabled: false,
    ghostClass: "ghost",
  };
});
</script>

<style scoped>
.b {
  border: 1px solid black;
}
.list-header {
  border-top-right-radius: 0.3rem;
  border-top-left-radius: 0.3rem;
  flex-grow: 1;
}
.list-group {
  border-top-right-radius: 0.3rem;
  border-top-left-radius: 0.3rem;
  padding: 5px;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
</style>
