<template>
  <div class="block form">
    <form>
        <h2>Добавление товара</h2>
        <div class="box">

            <p class="label">Наименование товара</p>
            <BaseComp
              class="base-input"
              v-model="name"
              label="Введите наименование товара"
              type="text"
              aria-required="true"
              @blur="onBlurName()"
              v-bind:class="{'invalid' : nameError}"
            />
            <p class="error" v-if="nameError">Поле является обязательным</p>

            <p class="label">Описание товара</p>
            <textarea
               class="base-input"
               name="review" 
               v-model="review"
               placeholder="Введите описание товара" 
               id="" 
               cols="30" 
               rows="10">
            </textarea>

            <p class="label image-link">Ссылка на изображение товара</p>
            <BaseComp
              class="base-input"
              v-model="url"
              label="Введите ссылку"
              type="url"
              aria-required="true"
              @blur="onBlurUrl()"
              v-bind:class="{'invalid' : urlError}"
            />
            <p class="error" v-if="urlError">Поле является обязательным</p>

            <p class="label">Цена товара</p>
            <BaseComp
              class="base-input"
              v-model="number"
              label="Введите цену"
              type="number"
              aria-required="true"
              @blur="onBlurPrice()"
              v-bind:class="{'invalid' : numberError}"
            />
            <p class="error" v-if="numberError">Поле является обязательным</p>

            <input 
              type="button" 
              value="Добавить товар" 
              class="btn"
              :disabled="!isDisabled"
              @click="sendForm()"
            >
        </div>
    </form>
  </div>
</template>

<script>
import BaseComp from '@/components/BaseComp.vue';
import UniqueID from '../components/UniqueId'
export default {
  components: {
    BaseComp
  },    
  data() {
      return {
          name: '',
          nameError: false,

          url: '',
          urlError: false,

          number: '',
          numberError: false,

          products: []
      }
  },
  methods: {
      sendForm() {
        this.products.push({ id: this.uuid,
                             name: this.name, 
                             review: this.review,
                             image: this.url, 
                             price: this.number})
                             

        let [num] = this.products[0].price.match(/^(.*?)((?:[,.]\d+)?|)$/);
        this.products[0].price = `${num.replace(/\B(?=(?:\d{3})*$)/g, ' ')}`;

        console.log(this.products[0].price)
        this.eventBus.emit('emit', this.products[0])
        this.products = [];
      },
      onBlurName() {
        if (this.name == '') {
          this.nameError = true;
        } else {
          this.nameError = false;
        }
      },
      onBlurUrl() {
        if (this.url == '') {
          this.urlError = true;
        } else {
          this.urlError = false;
        }
      },
      onBlurPrice() {
        if (this.number == '') {
          this.numberError = true;
        } else {
          this.numberError = false;
        }
      }
      
  },
  setup() {
        const uuid = UniqueID().getID()
        return {
            uuid
        }
  },
  computed: {
      isDisabled() {
          if (this.name != '' &&
              this.url != '' &&
              this.number != '') {
                  return true;
              } else {
                  return false;
              }
      }
  },
  name: 'FormView'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.form {
  width: 27%;

  form {
    display: flex;
    flex-direction: column;

    h2 {
      margin: 2.6rem 2.5rem;
      font-size: 2.2rem;
    }

    .box {
      margin: -1.2rem 1.8rem 2.7rem 2.7rem;;
      padding: 1.65rem 1.7rem;
      border: 0.1rem solid #FFFEFB;
      box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
      box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
      box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
      border-radius: 0.5rem;
      background-color: #FFFEFB;

      .label {
        font-size: .75rem;
        margin-top: -.09rem;
      }

      .base-input {
        position: relative;
        right: 1rem;
        width: 23rem;
        margin-top: .2rem;
        margin-bottom: 1.4rem;
        margin-left: 1rem;
        margin-right: 1rem;
        padding: .9rem 1.3rem;

        font-size: 1rem;
        font-style: normal;
        font-weight: 400;
        line-height: 15px;

        color: #B4B4B4;
        letter-spacing: -.02rem;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;

        &.invalid {
          border: 1px solid #FF8484;
        }
      }

      .image-link {
        margin-top: -0.7rem;
      }

      textarea {
        height: 9rem;
        resize: none;
        width: 100%;
      }

      .btn {
        background-color: #7BAE73;
        border-radius: 10px;
        width: 23rem;
        padding: .8rem 7.5rem;
        font-size: 1.1rem;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 600;
        line-height: 15px;
        
        text-align: center;
        letter-spacing: -0.02em;
        
        color: #FFFFFF;

        &:hover {
          transform: scale(90%);
          cursor: pointer;
        }

        &:disabled {
          background: #EEEEEE;
          color: #B4B4B4;
          cursor: not-allowed;

          &:hover {
            transform: scale(100%);
          }
        }
      }

      .error {
        position: relative;
        bottom: 1rem;
        color: #FF8484;
      }
    }
  }
}

@media (max-width:450px){

  .form {
    width: 27%;
  
    form {
      display: flex;
      flex-direction: column;
  
      h2 {
        margin: 2.6rem 2.5rem;
        width: 27rem;
        font-size: 3rem;
      }
  
      .box {
        flex-direction: column;
        margin: 2.8rem -0.2rem 4.7rem -12.3rem;
        height: 66rem;
        width: 59rem;
        display: flex;
        justify-content: center;
        padding: 1.65rem 1.7rem;
        border: 0.1rem solid #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 0.5rem;
        background-color: #FFFEFB;
  
        .label {
          position: relative;
          bottom: 5rem;
          font-size: 2.25rem;
          margin-top: 4.91rem;
          margin-left: 1rem;
        }
  
        .base-input {
          position: relative;
          align-self: center;
          right: 1rem;
          bottom: 5rem;
          width: 53rem;

          margin-top: .2rem;
          margin-bottom: 1.4rem;
          margin-left: 2rem;
          margin-right: 1rem;

          padding: .9rem 0.3rem;
          font-size: 2rem;
          font-style: normal;
          font-weight: 400;
          line-height: 15px;
          color: #B4B4B4;
          letter-spacing: -.02rem;
          background: #FFFEFB;
          box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
          border-radius: 4px;
  
          &.invalid {
            border: 1px solid #FF8484;
          }
        }
  
        .image-link {
          margin-top: -0.7rem;
        }
  
        textarea {
          height: 9rem;
          resize: none;
          width: 100%;
        }
  
        .btn {
          background-color: #7BAE73;
          border-radius: 10px;
          align-self: center;
          width: 36rem;
          padding: 1.8rem 7.5rem;
          font-size: 2.1rem;
          font-family: 'Inter';
          font-style: normal;
          font-weight: 600;
          line-height: 15px;
          text-align: center;
          letter-spacing: -0.02em;
          
          color: #FFFFFF;
  
          &:hover {
            transform: scale(90%);
            cursor: pointer;
          }
  
          &:disabled {
            background: #EEEEEE;
            color: #B4B4B4;
            cursor: not-allowed;
  
            &:hover {
              transform: scale(100%);
            }
          }
        }
  
        .error {
          position: relative;
          bottom: 1rem;
          color: #FF8484;
        }
      }
    }
  }
}
</style>
