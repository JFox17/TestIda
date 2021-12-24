<template>
  <div class="cards">
    <div
      class="cards_container"
      v-for="(card, i) in cards"
      :key="i"
    >
      <img :src="card.img" alt="картинка">
      <h4>{{card.name}}</h4>
      <p>{{card.description}}</p>
      <p>{{card.price}}</p>
    </div>
    <p>{{newCard}}</p>
  </div>
</template>
<script>
export default {
  props: ['newCard'],
  data() {
    return {
      name: '',
      description: '',
      price: '',
      cards: [
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Наименование товара',
          description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        }
      ]
    }
  },
  watch: {
    newCard: {
      // immediate: true, 
      handler (val) {
        this.cards.unshift(val)
      }
    }
    // 
  }
}
</script>
