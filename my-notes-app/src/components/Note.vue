<template>
  <div class="note">
     <Card style="width: 25rem; margin-bottom: 2em">
            <template #title class="note-control">
                <Button icon="pi pi-pencil" class="p-button-rounded p-button-secondary p-button-outlined" :disabled="!isActive" @click="editNote"/>
                <Button icon="pi pi-trash" class="p-button-rounded p-button-danger p-button-outlined" @click="$emit('delete-note', id)"/>
            </template>
            <template #content class="note-body">
                <textarea v-if="!isActive"
                          v-model="newNote"
                          @keyup.ctrl.enter="saveNote"
                          maxlength="200"
                ></textarea>
                <div
                    v-else
                    class="note-output"
                >{{!text ? newNote : text}}</div>

                <div class="note-footer">
                  <p class="char-counter">{{ !text ? characterCounter : text.length }} / 200</p>
                  <Button icon="pi pi-check" class="p-button-rounded p-button-success" :disabled="isActive || !newNote.length" @click="saveNote"/>
                </div>
            </template>
      </Card>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Card from "primevue/card";
import Button from "primevue/button";
// import NoteType from "../types/NoteType";

export default defineComponent({
  props: {
    id: Number,
    isActive: Boolean,
    text: String,
  },
  emits: ["note-active", "edit-note", "delete-note"],
  data() {
    return {
      newNote: "",
    };
  },
  components: {
    Card,
    Button,
  },
  methods: {
    saveNote() {
      this.$emit("note-active", this.id, this.newNote);
    },
    editNote() {
      this.$emit("edit-note", this.id);
    },
  },
  computed: {
    characterCounter() {
      return this.newNote.length;
    },
  },
});
</script>

<style scoped>
.p-card {
  min-width: 300px;
  padding: 2em 1em;
}
::v-deep(.p-card-title) {
  display: flex;
  gap: 0.5em;
  justify-content: flex-end;
}

textarea:active,
textarea:focus {
  outline-color: var(--grey);
}

textarea {
  border: 1px solid var(--grey);
}

textarea,
.note-output {
  width: 100%;
  min-height: 200px;
  font-size: 1.4rem;
  line-height: 2;
}
.note-output {
  font-weight: var(--bold);
  font-style: italic;
}
.note-footer {
  margin-top: 1em;
  display: flex;
  justify-content: space-between;
}
</style>
