<template>
  <div class="container">
    <create-card :onCard="onCard" />
    <cards :newCard="newCard" />
  </div>
</template>

<script>
import Cards from '../components/Cards.vue'
import CreateCard from '../components/CreateCard.vue'
export default {
  components: { 
    CreateCard,
    Cards 
  },
  data() {
    return {
      newCard: '',
    }
  },
  methods: {
    onCard(date) {
      this.newCard = date
      console.log(date)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  background: #E5E5E5;
  display: flex;
  padding: 32px;
}
</style>
