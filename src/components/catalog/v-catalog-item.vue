<template>
  <div class="v-catalog-item">
    <article class="v-catalog-item__card">

      <v-popup
          v-if="isPopupInfoVisible"
          rightBtnTitle="Add to cart"
          :popupTitle="product_data.name"
          @closePopup="closeInfoPopup"
          @rightBtnAction="addToCart"
      >
        <img
            class="v-catalog-item__image"
            :src="require('@/assets/images/' + product_data.image)"
            alt="img"
        >

        <div>
          <p class="v-catalog-item__name">{{ product_data.name }}</p>
          <p class="v-catalog-item__price">Price: {{ product_data.price }} ₽</p>
          <p class="v-catalog-item__price">{{ product_data.category }}</p>
        </div>
      </v-popup>
      <img
          class="v-catalog-item__image"
          :src="require('@/assets/images/' + product_data.image)"
          alt="img"
      >
      <p class="v-catalog-item__name">{{ product_data.name }}</p>
      <p class="v-catalog-item__price">Price: {{ product_data.price }} ₽</p>
      <button
        class="v-catalog-item__show-info"
        @click="showPopupInfo"
      >
        Show info
      </button>
      <button
          class="v-catalog-item__add-to-cart-btn btn"
          @click="addToCart"
      >Add to cart
      </button>
    </article>
  </div>
</template>

<script>
import vPopup from '../popup/v-popup'

export default {
  name: "v-catalog-item",
  components: {
    vPopup
  },
  props: {
    product_data: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  data() {
    return {
      isPopupInfoVisible: false
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', this.product_data)
    },
    showPopupInfo() {
      this.isPopupInfoVisible = true
    },
    closeInfoPopup() {
      this.isPopupInfoVisible = false
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