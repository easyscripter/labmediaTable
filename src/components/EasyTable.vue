<template>
  <table class="EasyTable">
    <thead class="EasyTable-header">
      <tr>
        <th class="IE-FlexAuto" v-for="(name, index) in columnsNameArray" :key="index">{{ name }}</th>
        <th class="deleteColumn"></th>
      </tr>
    </thead>
    <tbody class="EasyTable-body">
        <slot>Строка</slot>
    </tbody>
  </table>
</template>

<script>
'use strict'
export default {
  name: "EasyTable",
  props: {
    columnsName: {
      required: true,
      type: String,
    }
  },
  computed: {
    columnsNameArray: function () {
      return this.columnsName.split(",")
    },
  },
}
</script>

<style lang="scss" scoped>
    .EasyTable {
      display: flex;
      flex-wrap: wrap;
      max-width: 100%;
      justify-content: center;
      margin-left: 30px;
      margin-right: 30px;
      -webkit-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
      -moz-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
      box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);

      &-header {
        display: block;
        width: 100%;
        margin-top: 20px;

        tr {
          display: -webkit-flex;
          display: flex;
          width: 100%;
          padding: 10px 0;
          border-bottom: 1px solid rgba(34, 60, 80, 0.7);

          th {
            width: 300px;
            flex-basis: 25%;
            text-align: center;

            &:-ms-fullscreen, :root .IE-FlexAuto {
              flex-basis: auto;
            }
          }
        }
      }

      &-body {
        display: block;
        width: 100%;
      }
    }
</style>