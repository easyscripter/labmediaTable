<template>
<div class="easyfinder-container">
  <div class="input-container">
    <img src="../assets/icons/findIcon.svg" alt="find icon">
    <input  :placeholder="placeholderText" :value="value" @input="$emit('input', $event.target.value)">
  </div>
  <button class="easyfinder-clear-button" @click="$emit('input', $event.target.value = '')">Очистить фильтр</button>
</div>
</template>

<script>
export default {
name: "EasyFinder",
  props: {
    value: {
      type: String,
      required: true
    },
    placeholderText: {
      type: String
    }
  },
}
</script>

<style lang="scss" scoped>
    .easyfinder-container {
      position: relative;
      display: flex;
      flex-wrap: wrap;
      width: 100%;
      height: 120px;
      -webkit-box-shadow: 0px 10px 8px 0px rgba(34, 60, 80, 0.2);
      -moz-box-shadow: 0px 10px 8px 0px rgba(34, 60, 80, 0.2);
      box-shadow: 0px 10px 8px 0px rgba(34, 60, 80, 0.2);

      .input-container {
        width: 100%;
        position: relative;
        margin-top: 10px;
        input {
          width: 90%;
          height: 40px;
          padding-left: 40px;
          background-color: rgba(34, 60, 80, 0.2);
          border: none;
          border-radius: 8px;
          font-weight: bold;
          outline: none;
          &:focus  {
            color: #0b75d2;
            font-weight: bold;
          }
        }
        img {
          position: absolute;
          width: 20px;
          height: 20px;
          top: 10px;
          left: 55px;
        }
      }
      .easyfinder-clear-button {
        position: relative;
        background-color: transparent;
        margin-left: 10px;
        padding-left: 50px;
        border: none;
        cursor: pointer;
        outline: none;
        &::before {
          content: "";
          position: absolute;
          width: 20px;
          height: 20px;
          left: 20px;
          top: 50%;
          transform: translateY(-50%);
          background: url("../assets/icons/broom.svg");
        }
      }
    }
</style>