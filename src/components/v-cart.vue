<template>
  <div class="v-cart">
    <router-link
        :to="{ name: 'catalog'}"
    >
      <div class="v-cart__link-to-catalog">Back to catalog</div>
    </router-link>
    <h1>Cart</h1>
    <p v-if="!cart_data.length">There are no products in cart...</p>
    <v-cart-item
        v-for="(item, index) in cart_data"
        :key="item.article"
        :cart_item_data="item"
        @deleteFromCart="deleteFromCart(index)"
        @increment="increment(index)"
        @decrement="decrement(index)"
    />
    <div class="v-cart__total">
      <p class="v-cart__total-name">Total:</p>
      <p>{{ cartTotalCost }} ₽</p>
    </div>
  </div>
</template>

<script>
import vCartItem from './v-cart-item'
import {mapActions} from 'vuex'

export default {
  name: "v-cart",
  components: {
    vCartItem
  },
  props: {
    cart_data: Array,
    default() {
      return []
    }
  },
  data() {
    return {}
  },
  computed: {
    cartTotalCost() {
      let result = [];

      if (this.cart_data.length) {
        for (let item of this.cart_data) {
          result.push(item.price * item.quantity)
        }

        result = result.reduce(function(sum, el) {
          return sum + el;
        })
        return result;
      } else {
        return 0
      }
    }
  },
  methods: {
    ...mapActions([
      'DELETE_FROM_CART',
      'INCREMENT_CART_ITEM',
      'DECREMENT_CART_ITEM'
    ]),
    increment(index) {
      this.INCREMENT_CART_ITEM(index)
    },
    decrement(index) {
      this.DECREMENT_CART_ITEM(index)
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index)
    }
  },
  watch: {},
  mounted() {
  }

}
</script>

<style lang="scss">
.v-cart {
  margin-bottom: 100px;

  &__link-to-catalog {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: $padding*2;
    border: 1px solid #aeaeae;
  }

  &__total {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;

    display: flex;
    justify-content: center;
    padding: $padding*2 $padding*3;

    font-size: 20px;

    color: #FFF;
    background-color: $green-bg;

    &-name {
      margin-right: $margin*2;
    
    }
  }
}

</style>