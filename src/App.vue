<template>
  <div class="wrapper">
    <FormView/>
    <ProductsView/>
  </div>
</template>

<script>
import ProductsView from './views/ProductsView.vue';
import FormView from './views/FormView.vue'

export default {
  name: 'App',
  components: {
    ProductsView,
    FormView
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&display=swap');

* {
  font-family: 'Source Sans Pro', sans-serif;
  margin: 0;
  padding: 0;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  text-decoration: none;
  outline: none;
  border: none;
  -webkit-transition: all .2s linear;
  transition: all .2s linear;
}

html {
  overflow-x: hidden;
  font-size: 62.5%;
  width: 1150px;
  margin: 0 auto;
}

html::-webkit-scrollbar {
  width: 1rem;
}

html::-webkit-scrollbar-track {
  background-color: #FFFEFB;
}

body {
  background-color: #FFFEFB;
}

.wrapper {
  display: flex;
  flex-direction: row;
}

.block {
  height: 100%;
}

 @media (max-width:450px){
 
    .wrapper{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
 
 }
</style>
