<template>
  <div class="v-catalog-item">
    <article class="v-catalog-item__card">
      <img
          class="v-catalog-item__image"
          :src="require('@/assets/images/' + product_data.image)"
          alt="img"
      >
      <p class="v-catalog-item__name">{{ product_data.name }}</p>
      <p class="v-catalog-item__price">Price: {{ product_data.price }} ₽</p>
      <button
          class="v-catalog-item__add-to-cart-btn btn"
          @click="addToCart"
      >Add to cart
      </button>
    </article>
  </div>
</template>

<script>
export default {
  name: "v-catalog-item",
  props: {
    product_data: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', this.product_data)
    }
  },
  mounted() {
    this.$set(this.product_data, 'quantity', 1)
  }
}
</script>

<style lang="scss">
.v-catalog-item {
  width: 33.333333%;
  padding: 0 15px;
  margin-bottom: 30px;

  @media (max-width: 768px) {
    width: 50%;
  }

  @media (max-width: 767px) {
    width: 100%;
  }

  &__card {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    padding: $padding*2;
    margin-bottom: $margin*2;

    box-shadow: 0 0 8px 0 #e0e0e0;
  }

  &__add-to-cart-btn {
    margin-top: auto;
  }


  &__image {
    max-width: 100px;
  }
}

</style>