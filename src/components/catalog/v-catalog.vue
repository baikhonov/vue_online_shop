<template>
  <div class="v-catalog">
    <router-link
        :to="{ name: 'cart', params: {cart_data: CART}}"
    >
      <div class="v-catalog__link-to-cart">Cart: {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <div class="filters">
      <v-select
          :options="categories"
          :selected="selected"
          @select="sortByCategories"
      />

      <div class="range-slider">
        <input
            type="range"
            min="0"
            max="1000"
            step="10"
            v-model.number="minPrice"
            @change="setRangeSlider"
        >
        <input
            type="range"
            min="0"
            max="1000"
            step="10"
            v-model.number="maxPrice"
            @change="setRangeSlider"
        >
      </div>

      <div class="range-values">
        <p>Min: {{ minPrice }}</p>
        <p>Max: {{ maxPrice }}</p>
      </div>
    </div>

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
import {mapActions, mapGetters} from 'vuex'

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  data() {
    return {
      categories: [
        {name: 'Все', value: 'all'},
        {name: 'Мужские', value: 'm'},
        {name: 'Женские', value: 'w'}
      ],
      selected: 'Все',
      sortedProducts: [],
      minPrice: 0,
      maxPrice: 1000
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
    setRangeSlider() {
      if (this.minPrice > this.maxPrice) {
        let tmp = this.maxPrice;
        this.maxPrice = this.minPrice;
        this.minPrice = tmp;
      }
      this.sortByCategories();
    },
    sortByCategories(category) {
      let vm = this;
      this.sortedProducts = [...this.PRODUCTS];
      this.sortedProducts = this.sortedProducts.filter(function (item) {
        return item.price >= vm.minPrice && item.price <= vm.maxPrice;
      })
      if (category) {
        this.sortedProducts = this.sortedProducts.filter(function (e) {
          vm.selected = category.name;
          return e.category === category.name
        })
      }
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
        .then((response) => {
          if (response.data) {
            console.log('Data arrived!');
            this.sortByCategories()
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

.filters {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 50px;
}

.range-slider {
  position: relative;

  width: 200px;
  margin: auto 16px;

  text-align: center;

  & svg,
  & input[type=range] {
    position: absolute;
    left: 0;
    bottom: 0;
  }

  & input[type=range]::-webkit-slider-thumb {
    z-index: 2;
    position: relative;
    top: 2px;
    margin-top: -4px;
  }

}

</style>