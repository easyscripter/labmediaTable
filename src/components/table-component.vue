<template>
<div class="table-container">
  <table>
    <tr>
      <th v-for="(name, index) in columnsNameArray" :key="index">{{name}}</th>
    </tr>
    <table-row v-for="(user, index) in users" :key="index">
      <td class="username">{{user.username}}</td>
      <td>{{user.email}}</td>
      <td>{{formatedDate(user.registration_date)}}</td>
      <td>{{user.rating}}</td>
    </table-row>
  </table>
</div>
</template>

<script>
import tableRow from "@/components/tableRow-component"
export default {
  name: "table-component",
  components: {
    tableRow
  },
  props: {
    columnsName: {
      required: true,
      type: String,
    }
  },
  data: () => {
    return {
      users: [
        {
          id:1,
          username: "Sister_Swift",
          email:"Vicente48@hotmail.com",
          registration_date:"2020-03-28T19:50:24.665Z",
          rating:72
        },
        {
          id:2,
          username:"Tate_Stokes82",
          email:"Adonis_Bashirian18@yahoo.com",
          registration_date:"2020-06-06T07:01:15.412Z",
          rating:68
        }
      ]
    }
  },
  computed: {
    columnsNameArray: function () {
      return this.columnsName.split(",")
    },
  },
  methods: {
    formatedDate(date) {
      date = new Date(date);
      let Day = date.getDate();
      let Month = date.getMonth();
      let Year = date.getFullYear() % 100;
      if (Day < 10) Day = `0${Day}`
      if (Month < 10) Month = `0${Month}`
      if (Year < 10) Year = `0${Year}`

      return `${Day}.${Month}.${Year}`
    }
  }
}
</script>

<style lang="scss" scoped>
  .table-container {
    width: 100%;
    display: flex;
    table {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      width: 100%;
      margin: 30px;
      -webkit-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      -moz-box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      box-shadow: 0px 4px 8px 0px rgba(34, 60, 80, 0.2);
      tr {
        display: flex;
        width: 100%;
        padding: 0 15px;
        border-bottom: 1px solid #aaa9a9;
        th {
          color: #aaa9a9;
          padding: 20px 0;
          flex-basis: 25%;
          text-align: left;
        }
        td {
          padding: 20px 0;
          flex-basis: 25%;
          text-align: left;
        }
        .username {
          color: #47aaff;
          font-weight: bold;
        }
      }
    }
  }
</style>