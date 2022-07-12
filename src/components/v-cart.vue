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
    />
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
  computed: {},
  methods: {
    ...mapActions([
      'DELETE_FROM_CART'
    ]),
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

  &__link-to-catalog {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: $padding*2;
    border: 1px solid #aeaeae;
  }
}

</style>