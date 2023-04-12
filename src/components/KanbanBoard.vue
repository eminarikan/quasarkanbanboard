<template>
  <q-card flat class="full-width">
    <q-card-actions align="left">
      <q-btn dense color="primary" icon="add" label="Yeni" />
      <q-toggle v-model="darkMode" color="green" label="Dark" />
    </q-card-actions>
    <q-card-section class="row justify-start full-width">
      <div class="col q-ma-sm" v-for="(column, key) in columns" :key="key">
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
                :class="`bg-${column.color} text-white row justify-between rounded-borders`"
              >
                <q-item-label class="text-caption">
                  {{ column.list.length + " " + column.label }}
                </q-item-label>
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
            <div class="q-pa-sm">
              <q-card flat bordered class="" style="cursor: move">
                <q-card-section class="flex justify-between">
                  <div>{{ element.id }}</div>
                  <q-chip icon="person" :label="element.name" />
                  <q-btn-dropdown flat dense dropdown-icon="more_vert">
                    <q-list>
                      <q-item
                        dense
                        clickable
                        v-close-popup
                        @click="onItemClick"
                      >
                        <q-item-section avatar>
                          <q-icon color="warning" name="edit" />
                        </q-item-section>
                        <q-item-section>
                          <q-item-label>Güncelle</q-item-label>
                        </q-item-section>
                      </q-item>
                      <q-item
                        dense
                        clickable
                        v-close-popup
                        @click="onItemClick"
                      >
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
                <q-card-section class="flex justify-between">
                  <div>{{ element.description }}</div>
                </q-card-section>
              </q-card>
            </div>
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

const lightModeStyle = "bg-blue-grey-2 rounded-borders";
const darkModeStyle = "bg-blue-grey-8 rounded-borders";

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
  opacity: 0.3;
  background: #f2c037;
}
</style>
