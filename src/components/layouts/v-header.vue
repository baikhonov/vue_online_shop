<template>
  <div class="v-header">
    <router-link
        :to="{ name: 'mainPage'}"
    >
      <img class="v-header__logo" src="@/assets/logo.png" alt="Logo">
    </router-link>
    <div class="v-header__search">
      <input
          class="v-header__search-input"
          type="text"
          v-model="searchValue"
      >
      <button
          class="v-header__search-btn"
          @click="search(searchValue)"
      >
        <i class="material-icons">search</i>
      </button>
      <button
          class="v-header__search-btn v-header__search-btn--clear"
          @click="clearSearchField"
      >
        <i class="material-icons">clear</i>
      </button>
    </div>
  </div>
</template>

<script>
import {mapActions, mapGetters} from 'vuex'

export default {
  name: "v-header",
  data() {
    return {
      searchValue: ''
    }
  },
  computed: {
    ...mapGetters([
      'SEARCH_VALUE'
    ])
  },
  methods: {
    ...mapActions([
      'GET_SEARCH_VALUE_TO_VUEX'
    ]),
    search(value) {
      this.GET_SEARCH_VALUE_TO_VUEX(value);
      if (this.this.$router.path !== '/catalog') {
        this.$router.push('/catalog');
      }
    },
    clearSearchField() {
      this.searchValue = '';
      this.GET_SEARCH_VALUE_TO_VUEX();
      if (this.this.$router.path !== '/catalog') {
        this.$router.push('/catalog');
      }
    }
  }
}
</script>

<style lang="scss">
.v-header {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 1;

  display: flex;
  justify-content: space-between;
  align-items: center;

  width: 100%;
  background-color: $green-bg;
  padding: 16px;

  &__logo {
    width: 50px;
  }

  &__search {
    display: flex;

    &-input {
      padding: $padding $padding*4 $padding $padding;
      border: none;
      border-radius: $radius;
    }

    &-btn {
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      margin-left: 16px;

      background-color: transparent;
      border: none;

      &--clear {
        right: 38px;
      }
    }
  }
}
</style>