<template>
  <div class="create-cards">
    <div class="create-cards_container">
      <input v-model="img">
      <input v-model="name">
      <input v-model="description">
      <input v-model="price">
      <button @click="addCard()">add</button>
    </div>
  </div>
</template>
<script>
export default {
  props:['onCard'],
  data() {
    return {
      img: '',
      name: '',
      description: '',
      price: ''
    }
  },
  methods: {
    addCard() {
      this.onCard({
        img: this.img,
        name: this.name,
        description: this.description,
        price: this.price
      })
    }
  }
}
</script>