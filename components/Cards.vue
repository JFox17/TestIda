<template>
  <div class="wrap">
    <div class="sort">
      <button class="sort__field" @click="openList"> {{ this.select }}
        <span>
          <svg  :class="[isOpen ? 'sort__arrow-active' : 'sort__arrow' ]" xmlns="http://www.w3.org/2000/svg" width="8" height="6" viewBox="0 0 8 6" fill="none">
            <path d="M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264" stroke="#B4B4B4"/>
          </svg>
        </span>
      </button>
      <ul class="sort__list" :class="[isOpen ? 'sort__list-active' : '' ]">
        <li @click="sortByBase()" >По умолчанию 
          <span >
          <svg :class="[isOpen ? 'sort__arrow-active' : 'sort__arrow' ]" xmlns="http://www.w3.org/2000/svg" width="8" height="6" viewBox="0 0 8 6" fill="none">
            <path d="M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264" stroke="#B4B4B4"/>
          </svg>
        </span>
        </li>
        <li @click="sortByMinPrice()">По цене min</li>
        <li @click="sortByMaxPrice()">По цене max</li>
        <li @click="sortByName()">По наименованию</li>
      </ul>
    </div>
    <div class="cards">
      <div
        class="cards__container"
        v-for="(card, i) in cards"
        :key="i"
      >
      <div class="cards__frame">
        <img
          class="cards__img"
          :src="card.img"
          alt="картинка"
        >
      </div>
        <div class="cards__block">
          <h4 class="cards__name">{{card.name}}</h4>
          <p class="cards__description">{{card.description}}</p>
          <p class="cards__price">{{card.price}}</p>
        </div>
        <div @click="removeCard(card)" class="cards__busket">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16" fill="none">
            <g clip-path="url(#clip0_4_349)">
            <path d="M10.207 5.79688C9.99998 5.79688 9.83224 5.96462 9.83224 6.17158V13.2535C9.83224 13.4604 9.99998 13.6283 10.207 13.6283C10.4139 13.6283 10.5817 13.4604 10.5817 13.2535V6.17158C10.5817 5.96462 10.4139 5.79688 10.207 5.79688Z" fill="white"/>
            <path d="M5.78544 5.79688C5.57848 5.79688 5.41074 5.96462 5.41074 6.17158V13.2535C5.41074 13.4604 5.57848 13.6283 5.78544 13.6283C5.99241 13.6283 6.16015 13.4604 6.16015 13.2535V6.17158C6.16015 5.96462 5.99241 5.79688 5.78544 5.79688Z" fill="white"/>
            <path d="M2.56294 4.76335V13.9953C2.56294 14.541 2.76303 15.0534 3.11256 15.4211C3.46048 15.7898 3.94467 15.9991 4.4514 16H11.541C12.0478 15.9991 12.532 15.7898 12.8798 15.4211C13.2293 15.0534 13.4294 14.541 13.4294 13.9953V4.76335C14.1242 4.57893 14.5745 3.90768 14.4815 3.19471C14.3884 2.48189 13.7811 1.94867 13.0622 1.94852H11.1437V1.48014C11.1459 1.08626 10.9902 0.708039 10.7113 0.42979C10.4325 0.151688 10.0537 -0.0031709 9.65982 4.92333e-05H6.33255C5.93867 -0.0031709 5.55986 0.151688 5.28103 0.42979C5.00219 0.708039 4.84646 1.08626 4.84865 1.48014V1.94852H2.93019C2.21122 1.94867 1.60393 2.48189 1.51084 3.19471C1.4179 3.90768 1.86813 4.57893 2.56294 4.76335V4.76335ZM11.541 15.2506H4.4514C3.81075 15.2506 3.31236 14.7002 3.31236 13.9953V4.79629H12.68V13.9953C12.68 14.7002 12.1816 15.2506 11.541 15.2506ZM5.59806 1.48014C5.59558 1.28503 5.67227 1.09724 5.81074 0.959502C5.94906 0.821768 6.13729 0.746095 6.33255 0.749461H9.65982C9.85508 0.746095 10.0433 0.821768 10.1816 0.959502C10.3201 1.09709 10.3968 1.28503 10.3943 1.48014V1.94852H5.59806V1.48014ZM2.93019 2.69793H13.0622C13.4347 2.69793 13.7367 2.99989 13.7367 3.3724C13.7367 3.74491 13.4347 4.04687 13.0622 4.04687H2.93019C2.55768 4.04687 2.25571 3.74491 2.25571 3.3724C2.25571 2.99989 2.55768 2.69793 2.93019 2.69793V2.69793Z" fill="white"/>
            <path d="M7.9962 5.79688C7.78923 5.79688 7.62149 5.96462 7.62149 6.17158V13.2535C7.62149 13.4604 7.78923 13.6283 7.9962 13.6283C8.20317 13.6283 8.37091 13.4604 8.37091 13.2535V6.17158C8.37091 5.96462 8.20317 5.79688 7.9962 5.79688Z" fill="white"/>
            </g>
          </svg>
        </div>
      </div>
    </div>
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
      isOpen: false,
      select: 'По умолчанию',
      cards: [
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Обормотик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '13 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Котик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '15 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Лапусик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '12 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Мяучкин',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Барсик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '9 010 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Шустрик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '9 732 руб.'
        }
      ],
      copyCards: [
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Обормотик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '13 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Котик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '15 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Лапусик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '12 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Мяучкин',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '10 000 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Барсик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '9 010 руб.'
        },
        {
          img: 'https://www.ptichka.ru/data/cache/2018jan/13/57/49869_74018.jpg',
          name: 'Шустрик',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.',
          price: '9 732 руб.'
        }
      ]
    }
  },
  methods: {
    openList() {
      if(this.isOpen === true) {
        this.isOpen = false
      }else {
        this.isOpen = true
      }
      
    },
    removeCard(card) {
      this.cards.splice(card, 1)
      this.copyCards.splice(card, 1)
    },
    sortByBase() {
      this.cards = this.copyCards
      this.select = 'По умолчанию'
      this.isOpen = false
    },
    sortByMinPrice() {
      this.cards = this.copyCards
      const temp = JSON.parse(JSON.stringify(this.cards))

      temp.forEach(element => {
        element.price = +element.price.replace(/\D/g, '')
      });

      temp.sort((a, b) => a.price - b.price)
      this.cards = temp
      this.select = 'По цене min'
      this.isOpen = false
      
    },
    sortByMaxPrice() {
      this.cards = this.copyCards

      const temp = JSON.parse(JSON.stringify(this.cards))

      temp.forEach(element => {
        element.price = +element.price.replace(/\D/g, '')
      });

      temp.sort((a, b) => b.price - a.price)
      this.cards = temp
      this.select = 'По цене max'
      this.isOpen = false
      
    },
    sortByName() {
      this.cards = this.copyCards

      const temp = JSON.parse(JSON.stringify(this.cards))

      temp.sort((a, b) => a.name > b.name ? 1: -1)
      this.cards = temp
      this.select = 'По наименованию'
      this.isOpen = false
    }
  },
  watch: {
    newCard: {
      handler (val) {
        this.cards.unshift(val)
        this.copyCards.unshift(val)
      }
    }
  }
}
</script>
<style lang="scss">
.wrap {
  font-family: Source Sans Pro;
  font-style: normal;
}
.cards {
  color: #3F3F3F;
  text-align: left;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;

  &__container {
    max-width: 332px;
    margin: 8px 0;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    position: relative;
    cursor: pointer;
  }
  &__img {
    width: 100%;
    height: 100%;
    border-radius: 4px 4px 0px 0px;
  }
  &__name {
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    margin: 16px 0;
  }
  &__description {
    font-weight: normal;
    font-size: 16px;
    line-height: 20px;
    margin-bottom: 32px;
  }
  &__price {
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
  }
  &__busket {
    background: #FF8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    width: 32px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: -7px;
    right: -7px;
    transition: 0.1s all linear;
    opacity: 0;
    visibility: hidden;
  }
  &__block {
    padding: 0 16px 24px 16px;
  }
  &__container:hover &__busket {
    opacity: 1;
    visibility: visible;
    transition: .55s opacity, .55s visibility;
  }
  &__frame {
    height: 200px;
  }
}
.sort {
  font-weight: normal;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  cursor: pointer;
  position: relative;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 8px;

  &__field {
    background: #FFFEFB;
    border-radius: 4px;
    padding: 10px 0;
    min-width: 130px;
  }
  &__list {
    background: #FFFEFB;
    color: #B4B4B4;
    list-style: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    transition: all 0.8s cubic-bezier(0.165, 0.84, 0.44, 1);
    position: absolute;
    max-height:0px;
    overflow:hidden;
    transition: max-height 0.8s linear;
    z-index: 1;
    top: 1px;
    border-radius: 4px;
    li {
      padding: 10px 16px;
    }
    li:hover {
      background: #e5e5e573;
      transition: 0.5s;
      color: black;
    }
  }
  &__list-active {
    max-height:300px;
  }
  &__arrow-active {
    transition: transform .8s ease-in-out;
    transform: rotate(180deg);
  }
  &__arrow {
    transition: transform .8s ease-in-out;
    transform: rotate(0deg);
  }
}
</style>
