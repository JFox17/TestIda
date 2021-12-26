<template>
  <div class="unite">
    <div class="unite__container">
      <create-card :onCard="onCard" />
      <div class="lds-roller" :class="[isReady ? 'loader' : '']">
        <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
      </div>
      <cards :newCard="newCard" @ready="onReady" :class="[isReady ? '' : 'loader']"/>
    </div>
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
      isReady: false,
    }
  },
  methods: {
    onCard(date) {
      this.newCard = date
    },
    onReady(date) {
      this.isReady = date
    }
  }
}
</script>

<style lang="scss">
.unite {
  background: #E5E5E5;
  &__container {
    margin: 0 auto;
    display: flex;
    padding: 32px;
    max-width: 1200px;
    @media (max-width: 768px) { 
      flex-direction: column;
    }
  }
}

.loader {
  display: none !important;
}
 .lds-roller {
	display: block;
	position: relative;
	width: 80px;
	height: 80px;
	margin: 0 auto 25px auto;
	padding-top: 20px;
}
.lds-roller div {
	animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
	transform-origin: 40px 40px;
}
.lds-roller div:after {
	content: " ";
	display: block;
	position: absolute;
	width: 7px;
	height: 7px;
	border-radius: 50%;
	background: #b6b8bd;
	margin: -4px 0 0 -4px;
}
.lds-roller div:nth-child(1) {
	animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
	top: 63px;
	left: 63px;
}
.lds-roller div:nth-child(2) {
	animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
	top: 68px;
	left: 56px;
}
.lds-roller div:nth-child(3) {
	animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
	top: 71px;
	left: 48px;
}
.lds-roller div:nth-child(4) {
	animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
	top: 72px;
	left: 40px;
}
.lds-roller div:nth-child(5) {
	animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
	top: 71px;
	left: 32px;
}
.lds-roller div:nth-child(6) {
	animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
	top: 68px;
	left: 24px;
}
.lds-roller div:nth-child(7) {
	animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
	top: 63px;
	left: 17px;
}
.lds-roller div:nth-child(8) {
	animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
	top: 56px;
	left: 12px;
}
@keyframes lds-roller {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}
</style>
