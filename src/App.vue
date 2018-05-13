<template>
  <div id="app">
    
        <navbar />
      

    <div class="row" style="margin-top: 100px;">
      <div class="col l9">
        <productlist v-for="product in products" :key="product.id" :id="product.id" :name="product.name" :image="product.image" :price="product.price" />
      </div>
      <div class="col l3">
        <shoppingcart />
      </div>
    </div>

   

    
      
  </div>
</template>

<script>
import productlist from './productlist.vue';
import shoppingcart from './shoppingcart.vue';
import navbar from './navbar.vue';


export default {
  name: 'app',
  computed: {
    products() { return this.$store.getters.products; }
  },
  components: {
    productlist,
    shoppingcart,
    navbar
  }
}
</script>

<style>
  .cartIcon {
    padding: 5px;
  }
</style>
