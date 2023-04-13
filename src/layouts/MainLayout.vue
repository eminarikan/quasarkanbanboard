<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="b">
      <q-toolbar>
        <q-toolbar-title> Kanban Component </q-toolbar-title>
        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup></script>
<style scoped>
.b {
  background: linear-gradient(
    90deg,
    rgba(27, 115, 184, 1) 0%,
    rgba(129, 177, 168, 1) 100%
  );
}
</style>
