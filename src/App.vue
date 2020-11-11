<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="glossy">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
          icon="menu"
        />

        <q-toolbar-title>Test Project</q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <Sidebar v-model="leftDrawerOpen" />

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Sidebar from "./components/sidebar/Sidebar.vue";
import ToggleButton from "./components/general/ToggleButton.vue";

@Component({
  components: {
    ToggleButton,
    Sidebar,
  },
})
export default class App extends Vue {
  leftDrawerOpen = false;
}
</script>

<style>
</style>
