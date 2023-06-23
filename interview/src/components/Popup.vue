<template>
    <div class="popup-overlay">
      <div class="popup">
        <h2>Add New Project</h2>
        <form @submit="submitForm">
          <div class="form-group">
            <label for="customerName">Customer Name</label>
            <input type="text" id="customerName" v-model="customerName" required />
          </div>
          <div class="form-group">
            <label for="projectName">Project Name</label>
            <input type="text" id="projectName" v-model="projectName" required />
          </div>
          <div class="form-actions">
            <button type="submit">Add Project</button>
            <button type="button" @click="cancel">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </template>
  
<script lang="ts">
  import { defineComponent } from 'vue';  
  export default defineComponent({
    data() {
      return {
        customerName: '',
        projectName: ''
      };
    },
    methods: {
      submitForm() {
        const newProject = {
          id: null, // You can assign a unique ID or generate it based on your requirements
          customerName: this.customerName,
          projectName: this.projectName,
          createdAt: new Date().toISOString()
        };
        this.$emit('addProject', newProject);
        this.cancel();
      },
      cancel() {
        this.customerName = '';
        this.projectName = '';
        this.$emit('closePopup');
      }
    }
  });
</script>
