<template>
  <div class="v-select">
    <p
        class="v-select__title"
        @click="areOptionsVisible = !areOptionsVisible"
    >{{ selected }}</p>
    <div
        class="v-select__options"
        v-if="areOptionsVisible || isExpanded"
    >
      <p
          v-for="option in options"
          :key="option.value"
          @click="selectOption(option)"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select",
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default: ''
    },
    isExpanded: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      areOptionsVisible: false
    }
  },
  methods: {
    selectOption(option) {
      this.$emit('select', option)
      this.areOptionsVisible = false
    },
    hideSelect(evt) {
      if (!document.querySelector(".v-select").contains(evt.target)) {
        this.areOptionsVisible = false;
      }
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true)
  },
  beforeDestroy() {
    document.removeEventListener('click', this.hideSelect)
  }
}
</script>

<style lang="scss">
.v-select {
  position: relative;
  width: 200px;
  margin-bottom: 20px;

  cursor: pointer;

  p {
    padding: 5px;
    margin: 0;
  }

  &__title {
    border: 1px solid #aeaeae;

    user-select: none;
  }

  &__options {

    background-color: #fff;
    border: 1px solid #aeaeae;
    position: absolute;
    top: 35px;
    right: 0;
    width: 100%;

    p {

      &:hover {
        background-color: #e7e7e7;
      }
    }
  }
}

</style>