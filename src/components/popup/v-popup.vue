<template>
  <div class="v-popup__overlay" ref="popupOverlay">
    <div class="v-popup">
      <div class="v-popup__header">
        <span>{{ popupTitle }}</span>
        <span>
          <i
              class="material-icons v-popup__btn"
              @click="closePopup"
          >close</i>
        </span>
      </div>
      <div class="v-popup__content">
        <slot></slot>
      </div>
      <div class="v-popup__footer">
        <button
            class="close-modal btn"
            @click="closePopup"
        >Close
        </button>
        <button
            class="submit-btn btn"
            @click="rightBtnAction"
        >{{ rightBtnTitle }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-popup",
  props: {
    popupTitle: {
      type: String,
      default: 'Popup name'
    },
    rightBtnTitle: {
      type: String,
      default: 'OK'
    }
  },
  data() {
    return {}
  },
  computed: {},
  methods: {
    closePopup() {
      this.$emit('closePopup')
    },
    rightBtnAction() {
      this.$emit('rightBtnAction')
    }
  },
  mounted() {
    let vm = this
    document.addEventListener('click', function(item) {
      if (item.target === vm.$refs['popupOverlay']) {
        vm.closePopup()
      }
    })
  }
}
</script>

<style lang="scss">
 .v-popup {

   width: 400px;
   padding: 16px;

   background-color: #fff;
   box-shadow: 0 0 10px 0 #e7e7e7;

   &__btn {
     cursor: pointer;
   }

   &__overlay {
     position: fixed;
     left: 0;
     top: 0;
     right: 0;
     bottom: 0;
     z-index: 2;

     display: flex;
     justify-content: center;
     align-items: center;

     background-color: rgba(0, 0, 0, 0.6);
   }

   &__header,
   &__footer {
     display: flex;
     justify-content: space-between;
     align-items: center;
   }

   &__content {
     display: flex;
     justify-content: center;
     align-items: center;
   }
   
   .submit-btn {
     padding: 8px;
     
     color: #fff;
     background-color: #26ae68;
   }

   .close-modal {
     padding: 8px;

     color: #fff;
     background-color: red;
   }
 }
</style>