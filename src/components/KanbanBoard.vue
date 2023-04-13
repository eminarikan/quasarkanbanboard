<template>
  <q-card flat class="q-mt-xl" style="width: 96vw">
    <q-card-actions align="left">
      <q-btn dense unelevated color="primary" icon="add" label="Yeni" />
      <q-toggle v-model="darkMode" color="green" label="Dark" />
    </q-card-actions>
    <q-card-section
      class="q-pa-none row justify-center"
      style="min-width: 100%"
    >
      <div class="col-2 q-ma-sm" v-for="(column, key) in columns" :key="key">
        <draggable
          :class="q.dark.isActive ? darkModeStyle : lightModeStyle"
          v-model="column.list"
          v-bind="dragOptions"
          group="todos"
          @start="drag = true"
          @end="drag = false"
          item-key="id"
        >
          <template #header>
            <div>
              <q-bar
                :class="`row justify-between rounded-borders`"
                :style="`border-bottom: 3px solid ${column.color}; border-bottom-left-radius: 0; border-bottom-right-radius: 0;`"
              >
                <span class="text-overline">
                  {{ column.list.length + " " + column.label }}
                </span>
                <q-btn-dropdown flat round dense dropdown-icon="more_vert">
                  <q-list>
                    <q-item dense clickable v-close-popup @click="onItemClick">
                      <q-item-section avatar>
                        <q-icon color="warning" name="edit" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label>Etiketi Değiştir</q-item-label>
                      </q-item-section>
                    </q-item>
                    <q-item dense clickable v-close-popup @click="onItemClick">
                      <q-item-section avatar>
                        <q-icon color="positive" name="add" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label>Sütun Ekle/Çıkar</q-item-label>
                      </q-item-section>
                    </q-item>
                  </q-list>
                </q-btn-dropdown>
              </q-bar>
              <div>
                <q-btn
                  flat
                  dense
                  color="primary"
                  icon="add_circle"
                  label="Yeni Kayıt"
                  class="full-width text-caption q-mt-sm"
                  align="left"
                  @click="onClick"
                />
              </div>
            </div>
          </template>
          <template #item="{ element }">
            <q-card
              class="q-ma-sm"
              :style="`cursor: move; border-left: 3px solid ${element.priority.color}`"
            >
              <q-card-section class="q-pa-sm flex justify-between">
                <div class="">
                  <q-item-label class="text-caption text-bold">{{
                    "İş #" + element.id
                  }}</q-item-label>
                  <q-btn
                    flat
                    push
                    no-caps
                    align="left"
                    :label="element.name"
                    class="q-pa-none"
                  />
                </div>
                <q-btn-dropdown
                  flat
                  dense
                  size="md"
                  rounded
                  dropdown-icon="more_vert"
                >
                  <q-list>
                    <q-item dense clickable v-close-popup @click="onItemClick">
                      <q-item-section avatar>
                        <q-icon color="warning" name="edit" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label>Güncelle</q-item-label>
                      </q-item-section>
                    </q-item>
                    <q-item dense clickable v-close-popup @click="onItemClick">
                      <q-item-section avatar>
                        <q-icon color="negative" name="delete" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label>Sil</q-item-label>
                      </q-item-section>
                    </q-item>
                  </q-list>
                </q-btn-dropdown>
              </q-card-section>
              <q-card-section class="q-pa-sm">
                <q-scroll-area class="" style="width: auto; height: 5rem">
                  <div>{{ element.description }}</div>
                </q-scroll-area>
              </q-card-section>
              <q-card-section class="q-pa-sm flex justify-between items-center">
                <q-select
                  dense
                  options-dense
                  borderless
                  rounded
                  use-chips
                  hide-dropdown-icon
                  v-model="element.priority"
                  :options="priorities"
                >
                  <template #selected>
                    <q-chip
                      dense
                      class="text-white text-caption q-pa-sm"
                      :color="element.priority.color"
                      icon-right="arrow_drop_down"
                      :label="element.priority.label"
                    />
                  </template>
                </q-select>
                <q-avatar
                  v-if="element.assigned"
                  size="1.3rem"
                  font-size=".75rem"
                  color="teal"
                  text-color="white"
                  >{{ element.assigned }}</q-avatar
                >
              </q-card-section>
              <q-separator v-if="element.tags" />
              <q-card-section v-if="element.tags" class="q-pa-sm">
                <q-chip
                  dense
                  class="q-pa-sm"
                  size=".7rem"
                  icon="tag"
                  color="primary"
                  text-color="white"
                  v-for="(tag, i) in element.tags"
                  :key="i"
                  :label="tag"
                />
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
import { ref, defineProps, computed, watch } from "vue";
import { useQuasar } from "quasar";
import priorities from "./priorities.json";

const q = useQuasar();
const darkMode = ref(false);

const props = defineProps({
  columns: Array,
});

const drag = ref(false);

const dragOptions = computed(() => {
  return {
    animation: 300,
    group: "todos",
    disabled: false,
    ghostClass: "ghost",
  };
});

//const lightModeStyle = "bg-blue-grey-1 rounded-borders";
//const darkModeStyle = "bg-blue-grey-8 rounded-borders";
const lightModeStyle = "rounded-borders";
const darkModeStyle = "rounded-borders";

function onClick() {}

watch(darkMode, () => {
  q.dark.set(darkMode.value);
});
</script>

<style scoped>
.b {
  border: 1px solid black;
}
.ghost {
  opacity: 0.2;
  background: #6f3a72;
}
</style>
