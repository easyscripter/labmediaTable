<template>
<div class="table-container">
  <table class="EasyTable">
    <thead class="EasyTable-header">
      <tr>
        <th v-for="(name, index) in columnsNameArray" :key="index">{{name}}</th>
        <th class="deleteColumn"></th>
      </tr>
    </thead>
    <tbody class="EasyTable-body">
        <slot>Строка</slot>
    </tbody>
  </table>
</div>
</template>

<script>
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
  .table-container {
    width: 100%;
    display: flex;
    .EasyTable {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      width: 100%;
      margin: 30px;
      -webkit-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      -moz-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      &-header {
        display: block;
        width: 100%;
        margin-top: 20px;
        tr {
          display: flex;
          justify-content: space-around;
          width: 100%;
          padding: 10px 0;
          border-bottom: 1px solid rgba(34, 60, 80, 0.7);
          th {
            flex: 1;
            text-align: center;
          }
        }
      }
      &-body {
        display: block;
        width: 100%;
        tr {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin-top: 10px;
          -webkit-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
          -moz-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
          box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
        }
      }
    }
  }
</style>