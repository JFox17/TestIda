<template>
  <div class="create-cards">
    <div class="create-cards__container">
      <h3 class="create-cards__title">Добавление товара</h3>
      <div class="create-cards__form">
        <div class="create-cards__wrap">
          <p class="create-cards__name">
            Наименование товара <span class="create-cards__cicle" />
          </p>
          <textarea
            class="create-cards__field"
            v-model="name"
            :class="[isErrorName ? 'create-cards__field-error' : '']"
            placeholder="Введите наименование товара"
            @input="validateName"
          />
          <span :class="[isErrorName ? 'create-cards__text-error' : '']" class="create-cards__text">Поле является обязательным</span>
        </div>
        <div class="create-cards__wrap">
          <p class="create-cards__name">
            Описание товара
          </p>
          <textarea
            class="create-cards__field create-cards__field-wide"
            v-model="description"
            placeholder="Введите описание товара"
          />
        </div>
        <div class="create-cards__wrap">
          <p class="create-cards__name">
            Ссылка на изображение товара <span class="create-cards__cicle" />
          </p>
          <textarea
            class="create-cards__field"
            v-model="img"
            placeholder="Введите ссылку"
            :class="[isErrorImg ? 'create-cards__field-error' : '']"
            @input="validateImg"
          />
          <span :class="[isErrorImg ? 'create-cards__text-error' : '']" class="create-cards__text">Поле является обязательным</span>
        </div>
        <div class="create-cards__wrap">
          <p class="create-cards__name">
            Цена товара <span class="create-cards__cicle" />
          </p>
          <textarea
            class="create-cards__field"
            v-model="price"
            placeholder="Введите цену"
            :class="[isErrorPrice ? 'create-cards__field-error' : '']"
            @input="validatePrice"
            v-mask="mask"
          />
          <span :class="[isErrorPrice ? 'create-cards__text-error' : '']" class="create-cards__text">Поле является обязательным</span>
        </div>
        <button
          @click="addCard"
          class="create-cards__btn"
          :class="[isValid ? 'create-cards__btn-valid' : '']"
        >
          Добавить товар
        </button>
      </div>
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
      price: '',
      isErrorName: false,
      isErrorImg: false,
      isErrorPrice: false,
      isValid: false,
      mask: null,
    }
  },
  methods: {
    validateName () {
      if (this.name === '') {
        this.isErrorName = true
      } else {
        this.isErrorName = false
      }

      if (this.name !== '' && this.img !== '' && this.price !== ''){
        this.isValid= true
      }else {
        this.isValid= false
      }
    },
    validateImg () {
      if (this.img === '') {
        this.isErrorImg = true
      } else {
        this.isErrorImg = false
      }

      if (this.name !== '' && this.img !== '' && this.price !== ''){
        this.isValid= true
      }else {
        this.isValid= false
      }
    },
    validatePrice() {
      console.log(this.price.length)
      if (this.price.length < 2 && this.price.length < 6) {
        this.mask = "#руб."
      } else if (this.price.length > 4 && this.price.length < 6) {
        this.mask = "##руб."
      } else if (this.price.length > 5 && this.price.length < 7 ) {
        this.mask = "###руб."
      } else if(this.price.length > 7 && this.price.length < 9) {
        this.mask = "# ###руб."
      } else if (this.price.length > 9 && this.price.length < 11) {
        this.mask = "## ###руб."
      } else if (this.price.length > 10 && this.price.length < 12) {
        this.mask = "### ###руб."
      } else if (this.price.length > 11) {
        this.mask = "# ### ###руб."
      }

      if (this.price === '') {
        this.isErrorPrice = true
      } else {
        this.isErrorPrice = false
      }

      if (this.name !== '' && this.img !== '' && this.price !== ''){
        this.isValid= true
      } else {
        this.isValid= false
      }
    },
    addCard() {
      if (this.name !== '' && this.img !== '' && this.price !== ''){
        this.isValid= true
        this.onCard({
          img: this.img,
          name: this.name,
          description: this.description,
          price: this.price
        })
        this.img=''
        this.name=''
        this.description=''
        this.price=''
      }
    }
  }
}
</script>
<style lang="scss">
  .create-cards {
    font-family: Source Sans Pro;
    font-style: normal;
    color: #3F3F3F;
    min-width: 330px;
    @media (max-width: 1150px) {
      min-width: 260px;
    }

    &__title {
      font-weight: 600;
      font-size: 28px;
      line-height: 35px;
    }
    &__form {
      background: #FFFEFB;
      box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
      border-radius: 4px;
      margin: 16px 16px 0 0;
      padding: 24px;
      @media (min-width: 280px) and (max-width: 768px) {
        flex-wrap: wrap;
        display: flex;
        flex-direction: column;
        justify-content: center;
      }
      @media (min-width: 420px) and (max-width: 768px) { 
        max-height: 330px;
      }
    }
    &__field{
      font-weight: normal;
      font-size: 12px;
      line-height: 15px;
      max-width: 284px;
      min-height: 36px;
      width: 100%;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      margin-bottom: 16px;
      padding: 10px 0 0px 16px;
      word-wrap: break-word;
      word-break: break-all;
      resize: none;
      overflow: auto;
      transition: 0.7s;
      border: 1px solid #FFFEFB;
      @media (max-width: 768px) { 
        padding: 10px 0 0px 8px;
        min-height: 32px;
        font-size: 10px;
        line-height: 15px;
      }
      &:focus {
        background: rgb(211 211 211 / 20%);
        border: 1px solid rgb(211 211 211 / 20%);
      }
    }
    &__field-error {
      border: 1px solid #FF8484;
    }
    &__name {
      font-weight: normal;
      font-size: 10px;
      line-height: 13px;
      letter-spacing: -0.02em;
      margin-bottom: 4px;
      display: flex;
    }
    &__cicle {
      display: block;
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background:rgba(255, 132, 132, 1);
    }
    &__field-wide {
      min-height: 108px;
      height: 100%;
    }
    &__btn {
      font-weight: 600;
      font-size: 12px;
      line-height: 15px;
      text-align: center;
      letter-spacing: -0.02em;
      color: #B4B4B4;
      background: #EEEEEE;
      border-radius: 10px;
      width: 100%;
      padding: 10px 0 11px 0;
      transition: 0.9s;
      @media (max-width: 768px) {
        width: 40%;
      }
    }
    &__btn-valid {
      background: rgba(123, 174, 115, 1);
      color: #FFFFFF;
    }
    &__text {
      font-weight: normal;
      font-size: 8px;
      line-height: 10px;
      letter-spacing: -0.02em;
      color: #FF8484;
      opacity: 0;
      transition: .55s opacity;
      position: absolute;
      bottom: 6px;
      left: 0;
    }
    &__text-error {
      opacity: 1;
    }
    &__wrap {
      position: relative;
      @media (max-width: 768px) {
        margin-right: 15px;
      }
    }
  }
  
</style>
