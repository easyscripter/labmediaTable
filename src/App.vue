<template>
  <div id="app">
    <h1>Список пользователей</h1>
    <easy-finder v-model="filterValue" placeholder-text="Поиск по имени или email"></easy-finder>
    <easy-table columnsName="Имя пользователя, E-mail, Дата регистрации, Рейтинг" >
      <easyTable-row v-for="(user, index) in filterdUsers" :key="index" :rowValues="`${user.username},${user.email},${formatedDate(user.registration_date)},${user.rating}`" @deleteRow="deleteRow(index)"></easyTable-row>
    </easy-table>
  </div>
</template>

<script>
import axios from 'axios'
import EasyTable from "@/components/EasyTable"
import EasyTableRow from "@/components/EasyTable-row"
import EasyFinder from "@/components/EasyFinder"
export default {
  name: 'App',
  components: {
    EasyTable,
    EasyTableRow,
    EasyFinder,
  },
  data: () => {
    return {
      users: [],
      filterValue: ''
    }
  },
  computed: {
    filterdUsers() {
      if (!this.filterValue.length) return this.users;

      return this.users.filter(item => {
        if (item.username.toLowerCase().includes(this.filterValue.toLowerCase()) || item.email.toLowerCase().includes(this.filterValue.toLowerCase())) {
          return item;
        }
      });
    }
  },
  created() {
    axios.get("https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users")
    .then(response => {this.users = response.data})
    .catch(error => console.error(error));
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
    },
    deleteRow (index) {
      this.users.splice(index, 1);
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  h1 {
    text-align: left;
  }
}
</style>
