<template>
  <div class="block products">
    <div class="sortbox">По умолчанию &or;</div>
    <div class="box-container">
      <div class="box"  v-for="product in products"  :key="product.id">
              <div class="content">
                  <div class="main-img" :style="{ backgroundImage: `url(${product.image})`}"></div>
                  <h3>{{ product.name }}</h3>
                  <div class="review">{{ product.review }}</div>
                  <div ><span class="price">{{ product.price }} руб.</span></div>
              </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductsView',
  data() {
        return {
            products: []
        }
  },
  mounted() {
      if (this.products) {  
        this.products = JSON.parse(localStorage.getItem('products'));
      }

      this.eventBus.on('emit', (args) => {
        console.log(args)
        if (this.products) {
          this.products.push(args)
          const parsed = JSON.stringify(this.products);
          localStorage.setItem("products", parsed)
        } else {
          this.products = [args]
          const parsed = JSON.stringify(this.products);
          localStorage.setItem("products", parsed)
        }
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.products {
  width: 73%;
}
.sortbox {
  display: flex;
  justify-content: space-around;
  align-items: center;

  position: relative;
  margin: 2.4rem;
  width: 95.49px;
  height: 30px;
  left: 83%;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;

  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 15px;
  color: #B4B4B4;

  &:hover {
    cursor: pointer;
  }
}
.box-container {
  display: -ms-grid;
  display: grid;
  -ms-grid-columns: (minmax(25rem, 1fr))[auto-fit];
      grid-template-columns: repeat(auto-fit, minmax(25rem, 1fr));
  gap: 2rem;
}
.box {
  position: relative;
  bottom: 2rem;
  right: .9rem;
  width: 262px;
  height: 345px;
  
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &:hover {
    cursor: pointer;
    transform: scale(95%);
  }

  .main-img {
    width: 262px;
    height: 158px;
    background-size: 100%;
    position: relative;
    top: 1rem;
  }

  h3 {
    position: relative;
    margin: 2rem 1.5rem;
    font-size: 2rem;
  }

  .review {
    position: relative;
    margin: -1.1rem 1.5rem;
    font-size: 1.5rem;
  }

  .price {
    position: relative;
    top: 8.5rem;
    margin: -1.1rem 1.5rem;
    font-size: 1.9rem;
    font-weight: bold;
  }
}
@media (max-width:450px){
  .box-container {
    display: -ms-grid;
    display: grid;
    -ms-grid-columns: (minmax(50rem, 1fr))[auto-fit];
        grid-template-columns: repeat(auto-fit, minmax(50rem, 1fr));
    gap: 2rem;
  }
  .box {
    position: relative;
    bottom: 2rem;
    right: -15.35rem;
    width: 562px;
    height: 545px;
    
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
  
    .main-img {
      width: 562px;
      height: 258px;
      background-size: 100%;
      position: relative;
      top: 1rem;
    }
  
    h3 {
      position: relative;
      margin: 2rem 1.5rem;
      font-size: 5rem;
    }
  
    .review {
      position: relative;
      margin: -1.1rem 1.5rem;
      font-size: 3.5rem;
    }
  
    .price {
      position: relative;
      top: 8.5rem;
      margin: -1.1rem 1.5rem;
      font-size: 3.9rem;
      font-weight: bold;
    }
  }
}
</style>
