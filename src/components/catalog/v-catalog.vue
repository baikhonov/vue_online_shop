<template>
  <div class="v-catalog">
    <router-link
      :to="{ name: 'cart', params: {cart_data: CART}}"
    >
      <div class="v-catalog__link-to-cart">Cart: {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <v-select
      :options="categories"
      :selected="selected"
      :isExpanded="IS_DESKTOP"
      @select="sortByCategories"
    />
    <div class="v-catalog__list">
      <v-catalog-item
        v-for="product in filteredProducts"
        :key="product.article"
        :product_data="product"
        @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from './v-catalog-item'
import vSelect from '../v-select'
import { mapActions, mapGetters } from 'vuex'

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  data() {
    return {
      categories: [
        { name: 'Все', value: 'all'},
        { name: 'Мужские', value: 'm'},
        { name: 'Женские', value: 'w'}
      ],
      selected: 'Все',
      sortedProducts: []
    }
  },
  computed: {
    ...mapGetters([
        'PRODUCTS',
        'CART',
        'IS_MOBILE',
        'IS_DESKTOP',
    ]),
    filteredProducts() {
      if (this.sortedProducts.length) {
        return this.sortedProducts
      } else {
        return this.PRODUCTS
      }
    }
  },
  methods: {
    ...mapActions([
        'GET_PRODUCTS_FROM_API',
        'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data)
    },
    sortByCategories(category) {
      this.sortedProducts = []
      this.PRODUCTS.map((item) => {
        if (item.category === category.name) {
          this.sortedProducts.push(item)
        }
      })
      this.selected = category.name
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
    .then((response) => {
      if (response.data) {
        console.log('Data arrived!');
      }
    })
  }
}
</script>

<style lang="scss">
.v-catalog {

  &__list {
    display: flex;
    flex-wrap: wrap;

    margin-left: -15px;
    margin-right: -15px;
  }

  &__link-to-cart {
    position: absolute;
    top: 15px;
    right: 15px;
    padding: $padding*2;
    border: 1px solid #aeaeae;
  }
}

</style>