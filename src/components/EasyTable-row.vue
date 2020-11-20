<template>
 <tr class="EasyTable-row" >
   <td :class="{'username': index === 0}" v-for="(value, index) in rowsArray" :key="index">{{value}}</td>
   <td class="delete-row" @click="$emit('deleteRow')">X</td>
 </tr>
</template>

<script>
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
  td {
    flex: 1;
  }
</style>