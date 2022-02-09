<template>
 <div class="board-title">
      <h1>{{ title }}</h1>
      <Button label="Add note +" class="p-button-rounded p-button-success" @click="addNote"/>
    </div>
  <div class="notes-wrap">
    <Note
      v-for="note in notes"
      :key="note.id"
      :isActive="note.isActive"
      :id="note.id"
      :text="note.text"
      @note-active="changeNoteState"
      @edit-note="editNote"
      @delete-note="deleteNote"
    />
  </div>
</template>

<script lang="ts">
import NoteType from "@/types/NoteType";
import { defineComponent } from "vue";
import Note from "./Note.vue";
import Button from "primevue/button";

export default defineComponent({
  data() {
    return {
      notes: [
        { id: 1, text: "", isActive: false } as NoteType,
        // eslint-disable-next-line
      ] as Array<any>,
      title: "Add some Notes!",
    };
  },
  components: {
    Note,
    Button,
  },
  mounted() {
    if (localStorage.getItem("notes-list") as string) {
      this.notes = JSON.parse(localStorage.getItem("notes-list") as string);
    }
  },
  methods: {
    changeNoteState(id: number, newNote: string) {
      const note = this.notes.find((el) => el.id === id);
      note.isActive = !note.isActive;
      note.text = newNote;
      this.saveNotesToLocalStorage();
    },
    editNote(id: number) {
      const note = this.notes.find((el) => el.id === id);
      note.isActive = !note.isActive;
      this.saveNotesToLocalStorage();
    },
    deleteNote(id: number) {
      const index = this.notes.findIndex((el) => el.id === id);
      this.notes.splice(index, 1);
      this.saveNotesToLocalStorage();
    },
    addNote() {
      if (!this.notes[this.notes.length - 1].isActive) return;
      this.notes.push({
        id: this.notes.length + 1,
        text: "",
        isActive: false,
      } as NoteType);
      this.saveNotesToLocalStorage();
    },
    saveNotesToLocalStorage() {
      const parsed = JSON.stringify(this.notes);
      localStorage.setItem("notes-list", parsed);
    },
  },
});
</script>

<style scoped>
.notes-wrap {
  display: flex;
  gap: 2em;
  margin-top: 4em;
}
.board-title {
  display: flex;
  gap: 2em;
}
</style>