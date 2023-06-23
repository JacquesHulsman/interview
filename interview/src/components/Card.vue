<template>
    <div class="cards">
        <div class="customer-name">{{ cardData.customerName }}</div>
        <div class="project-name">{{ cardData.projectName }}</div>
        <div class="time-since-created">{{ timeSinceCreated }}</div>
    </div>
  </template>
  
  <script lang="ts">
  
export default {
  props: {
    cardData: {
      type: Object,
      required: true
    }
  },
  computed: {
    timeSinceCreated() {
      // Calculate the time difference from the current time
      const createdTime = new Date(this.cardData.createdAt).getTime();
      const currentTime = Date.now();
      const timeDiff = currentTime - createdTime;

      // Convert the time difference to a human-readable format
      const minutes = Math.floor(timeDiff / 60000);
      const hours = Math.floor(minutes / 60);
      const days = Math.floor(hours / 24);

      if (days > 0) {
        return `${days} days ago`;
      } else if (hours > 0) {
        return `${hours} hours ago`;
      } else {
        return `${minutes} minutes ago`;
      }
    }
  }
};
  </script>
