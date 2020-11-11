<template>
  <div class="home">
    <ToggleButton />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"; // @ is an alias to /src
import ToggleButton from "../components/general/ToggleButton.vue";
@Component({
  components: {
    ToggleButton,
  },
})
export default class Home extends Vue {}
</script>
