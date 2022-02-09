<template>
  <div>
				<Menubar :model="items" class="navbar">
					<template #start>
						<div><img alt="logo" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" height="40" class="mr-2"></div>
            <span class="brand">Notes App</span>
					</template>
          <template #end>
          </template>
				</Menubar>
			</div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import Menubar from "primevue/menubar";

export default defineComponent({
  name: "maneHeader",
  components: {
    Menubar,
  },
  data() {
    return {
      items: [],
    };
  },
});
</script>
<style scoped>
.navbar {
  padding: 1em 5em;
  font-size: 1.4rem;
  background-color: var(--teal-200);
  margin-bottom: 2em;
}
::v-deep(.p-menubar-start) {
  display: flex;
  max-width: 150px;
  gap: 1em;
  justify-content: space-between;
  align-content: center;
  align-items: center;
  font-size: 1.6rem;
  font-weight: var(--bold);
}
</style>