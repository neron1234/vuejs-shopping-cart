<template>
<div id="shopping-cart">

  <div class="cart-btn">
    <a class="waves-effect waves-light btn">Cart <span class="badge red">{{ cartLength }}</span></a>
  </div>

  <table v-for="(item, index) in cart">
    <tr>
      <td class="center-align center">{{ item.name }}</td>
      <td class="center-align center">{{ '$' + item.price }}</td>
      <td class="center-align center">
          <a class="waves-effect waves-light btn red" @click="removeFromCart(index)" style="padding-top: 5px;"><IosCloseIcon w="20" h="20" /></a>         
      </td>
    </tr>  
  </table>
  
  <table>
    <tr>
        <th>Total</th>
        <th>{{ '$' + total }}</th>
    </tr>   
  </table>

  <div class="card">
      <div class="card-action">
          <a class="waves-effect waves-light btn red">Checkout</a>
      </div>
  </div>

</div>
</template>

<script>
import IosCloseIcon from '../node_modules/vue-ionicons/dist/ios-close.vue'

export default {
  name: 'shoppingcart',
  computed: {
    inCart() { return this.$store.getters.inCart; },
    cartLength(){ return this.inCart.length; },
    cart(){
        return this.$store.getters.inCart.map((cartproduct) => {
            return this.$store.getters.products.find((itemForSale) => {
                return cartproduct === itemForSale.id;
            });
        });
    },
    total(){
        return this.cart.reduce((acc, cur) => acc + cur.price, 0);
    }
  },
  components: {
      IosCloseIcon
  },
  methods: {
      removeFromCart(index) {
          this.$store.dispatch('removeFromCart', index)
      }
  }
};

</script>

<style>
    table {
        width: 320px;
    }
    tr {
        width: 300px;
    }
    td {
        width: 90px;
        margin: auto;
        padding: 2px;
    }

</style>
