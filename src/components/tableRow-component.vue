<template>
 <tr>
   <slot></slot>
   <td class="delete-row" @click="$emit('deleteRow', this.$event)">X</td>
 </tr>
</template>

<script>
export default {
  name: "tableRow-component",
}
</script>

<style lang="scss" scoped>
  .delete-row {
    padding: 20px 15px;
    text-align: center;
    cursor: pointer;
  }
</style>