<template>
  <div>
    <button class="btn-new-project" @click="addNewProject">+ New Project</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  methods: {
    addNewProject() {
      this.$emit('add-new-project');
    }
  }
});
</script>