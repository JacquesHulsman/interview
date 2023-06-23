<template>
  <div class="screen">
    <div class="view">
      <header class="header">
        <h1 class="header-text">{{ msg }}</h1>  
      </header>
      <input class="search" v-model="searchTerm" placeholder="Search" @input="filterCards" />
      <div class="content">
        <div class="card-container">
          <Card v-for="card in sortedCards" :key="card.id" :cardData="card" />
        </div>
        <div class="new-project-container">
          <button class="btn-new-project" @click="openPopup">+ New Project</button>
        </div>
        <Popup v-if="showPopup" @addProject="addNewProject" @closePopup="closePopup" />
      </div>
    </div>
    <div class="main-navigation">
        <img class="icon" src="../assets/Projects.svg" alt="Icon" />
        <img class="icon" src="../assets/Customers.svg" alt="Icon" />
        <img class="icon" src="../assets/Company.svg" alt="Icon" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Card from './Card.vue';
import cardData from './cards.json';
import NewProjectButton from './New-Project-Button.vue';
import Popup from './Popup.vue';

interface CardData {
  id: number;
  customerName: string;
  projectName: string;
  createdAt: string;
}

export default defineComponent({
  props: {
    msg: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      cards: cardData as CardData[],
      sortedCards: [] as CardData[],
      showPopup: false,
      searchTerm: ''
    };
  },
  mounted() {
    this.sortCards();
  },
  methods: {
    sortCards() {
      this.sortedCards = this.cards.sort((a, b) => {
        const timeA = new Date(a.createdAt).getTime();
        const timeB = new Date(b.createdAt).getTime();
        return timeB - timeA;
      });
    },
    openPopup() {
      this.showPopup = true;
    },
    closePopup() {
      this.showPopup = false;
    },
    addNewProject(newProject: CardData) {
      this.cards.push(newProject);
      this.sortCards();
    },
    filterCards() {
      if (this.searchTerm === '') {
        // If search term is empty, display all cards
        this.sortedCards = this.cards;
      } else {
        // Filter cards based on search term
        const searchTermLower = this.searchTerm.toLowerCase();
        this.sortedCards = this.cards.filter(card => {
          const customerNameLower = card.customerName.toLowerCase();
          const projectNameLower = card.projectName.toLowerCase();
          return (
            customerNameLower.includes(searchTermLower) ||
            projectNameLower.includes(searchTermLower)
          );
        });
      }
    }
  },
  components: {
    Card,
    Popup,
    NewProjectButton
}
});
</script>

