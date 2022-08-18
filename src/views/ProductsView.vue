<template>
  <div class="block products">
    <input type="checkbox"/>
    <div class="box"  v-for="product in products" :key="product.id">
            <div class="image">
                <img :src="product.image" class="main-img" alt="">
            </div>
            <div class="content">
                <h3>{{ product.name }}</h3>
                <div class="price">{{ product.price }} <span>$399.99</span></div>
            </div>
        </div>
  </div>
</template>

<script>
export default {
  name: 'ProductsView',
  data() {
        return {
            products: [
                {
                    id: 1,
                    name: "smartphone",
                    price: "$249.99"
                },
                {
                    id: 2,
                    name: "camera",
                    price: "$249.99"
                }
            ]
        }
  },
  mounted() {
      this.products = JSON.parse(localStorage.getItem('products'));

      this.eventBus.on('emit', (args) => {
        console.log(args)
        this.products.push(args)
        const parsed = JSON.stringify(this.products);
        localStorage.setItem("products", parsed)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.products {
  width: 73%;
}
</style>
