<template>
  <div class="EasyModal">
    <div :style="{width: `${modalWidth}px`, height: `${modalHeight}px`}" class="easyModal_body">
      <div class="easyModal_header">
        <p class="easyModal_title">{{ modalTitle }}</p>
        <i class="easyModal_close-button" @click="$emit('close')">X</i>
      </div>
      <div class="easyModal_content">
        <slot name="easyModal_Content"></slot>
      </div>
      <div class="easyModal_footer">
        <slot name="easyModal_Footer"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EasyModal.vue",
  props: {
    modalTitle: {
      type: String,
      default: "Модальное окно"
    },
    modalWidth: {
      type: Number,
    },
    modalHeight: {
      type: Number,
    }
  },
}
</script>

<style lang="scss" scoped>
.EasyModal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.8);
  -webkit-transition: opacity 400ms ease-in;
  -moz-transition: opacity 400ms ease-in;
  transition: opacity 400ms ease-in;

  &_body {
    position: relative;
    max-width: 800px;
    max-height: 900px;
    background-color: #ffffff;
    border-radius: 5px;
  }

  &_header {
    position: relative;
    display: flex;
    align-items: center;
    padding-top: 20px;

    p.easyModal_title {
      position: absolute;
      left: 5%;
      font-weight: bold;
      text-transform: uppercase;
    }

    i.easyModal_close-button {
      position: absolute;
      right: 5%;
      cursor: pointer;
    }
  }

  &_content {
    display: flex;
    margin-top: 30px;
    margin-left: 5%;
  }

  &_footer {
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
  }
}

</style>