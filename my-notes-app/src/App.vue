<template>
  <Header />
  <div class="container">
    <NotesBoard />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Header from "./components/Header.vue";
import NotesBoard from "./components/NotesBoard.vue";

export default defineComponent({
  name: "App",
  components: {
    Header,
    NotesBoard,
  },
  emits: ["add-note"],
  data() {
    return {
      title: "Add Some Notes!",
    };
  },
  methods: {},
});
</script>

<style>
</style>
