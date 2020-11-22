<template>
 <tr class="EasyTable-row">
   <td class="IE-FlexAuto" :class="{'username': index === 0}" v-for="(value, index) in rowsArray" :key="index">
     {{ value }}
   </td>
   <td class="delete-row" @click="$emit('deleteRow')">X</td>
 </tr>
</template>

<script>
'use strict'
export default {
  name: "EasyTable-row",
  props: {
    rowValues: {
      type: String,
      required: true
    }
  },
  computed: {
    rowsArray: function () {
      return this.rowValues.split(",")
    },
  }
}
</script>

<style lang="scss" scoped>
.delete-row {
  padding: 20px 15px;
  text-align: center;
  cursor: pointer;
}

.username {
  color: #0b75d2;
  font-weight: bold;
}

tr {
  width: 100%;
  display: -webkit-flex;
  display: flex;
  align-items: center;
  margin-top: 10px;
  -webkit-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
  box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);

  td {
    width: 300px;
    flex-basis: 25%;
    text-align: center;

    &:-ms-fullscreen, :root .IE-FlexAuto {
      flex-basis: auto;
    }
  }
}
</style>