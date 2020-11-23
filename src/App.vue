<template>
  <div id="app">
    <h1>Список пользователей</h1>
    <easy-modal v-show="isActiveModal" modal-title="Удалить пользователя" :modal-width="400" :modal-height="200"
                @close="isActiveModal = false">
      <template v-slot:EasyModal_Content>
        <p>Вы уверены, что хотите
          удалить пользователя?</p>
      </template>
      <template v-slot:EasyModal_Footer>
        <button class="deleteUser-btn" @click="deleteRow(deleteUserIndex)">Да</button>
        <button class="cancel-btn" @click="isActiveModal = false">Нет</button>
      </template>
    </easy-modal>
    <easy-finder :style="{pointerEvents: isActiveModal ? 'none' : 'auto'}"
                 :show-button="!!(this.filterValue.length || this.activeSort.date || this.activeSort.rating)"
                 v-model="filterValue" placeholder-text="Поиск по имени или email"
                 @clearFilters="clearSortAndFilter"></easy-finder>
    <div :style="{pointerEvents: isActiveModal ? 'none' : 'auto'}" class="sort-container">Сортировка: <p
        :class="{active: activeSort.date}" @click="sortFromDate()">Дата регистрации</p>
      <p :class="{active: activeSort.rating}" @click="sortFromRating()">Рейтинг</p></div>
    <easy-table :style="{pointerEvents: isActiveModal ? 'none' : 'auto'}"
                columnsName="Имя пользователя, E-mail, Дата регистрации, Рейтинг">
      <easyTable-row v-for="(user, index) in filteredUsers" :key="index"
                     :rowValues="`${user.username},${user.email},${formattedDate(user.registration_date)},${user.rating}`"
                     @deleteRow="openDeleteModal(user.id)"></easyTable-row>
    </easy-table>
  </div>
</template>

<script>
'use strict'
import axios from 'axios'
import EasyTable from "@/components/EasyTable"
import EasyTableRow from "@/components/EasyTable-row"
import EasyFinder from "@/components/EasyFinder"
import EasyModal from "@/components/EasyModal"

export default {
  name: 'App',
  components: {
    EasyModal,
    EasyFinder,
    EasyTable,
    EasyTableRow,
  },
  data: () => {
    return {
      users: [],
      filterValue: '',
      reversedDateSortFlag: false,
      reversedRatingSortFlag: false,
      activeSort: {
        date: false,
        rating: false
      },
      sortedUsers: [],
      isActiveModal: false,
      deleteUserIndex: 0
    }
  },
  computed: {
    filteredUsers() {
      if (this.filterValue.length) {
        return this.sortedUsers.filter(item => {
          if (item.username.toLowerCase().includes(this.filterValue.toLowerCase().trim()) || item.email.toLowerCase().includes(this.filterValue.toLowerCase().trim())) {
            return item;
          }
        });
      } else if (!this.filterValue.length && !this.activeSort.date && !this.activeSort.rating) {
        return this.users;
      }
      return this.sortedUsers;
    },
  },
  created() {
    this.fetchUsers();
  },
  methods: {
    formattedDate(date) {
      date = new Date(date);
      let Day = date.getDate();
      let Month = date.getMonth() + 1;
      let Year = date.getFullYear() % 100;
      if (Day < 10) Day = `0${Day}`
      if (Month < 10) Month = `0${Month}`
      if (Year < 10) Year = `0${Year}`

      return `${Day}.${Month}.${Year}`
    },
    async fetchUsers () {
      await axios.get("https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users")
          .then(response => {
            this.users = response.data
          })
          .catch(error => console.error(error));
      this.sortedUsers = this.users.slice();
    },
    deleteRow (index) {
      this.users.splice(this.users.indexOf(this.users.find(item => item.id === index)), 1);
      this.sortedUsers.splice(this.sortedUsers.indexOf(this.sortedUsers.find(item => item.id === index)), 1);
      this.isActiveModal = false;
    },
    openDeleteModal(index) {
      this.deleteUserIndex = index;
      this.isActiveModal = true;
    },
    sortFromDate() {
      if (!this.reversedDateSortFlag) {
        this.sortedUsers.sort((first, second) => new Date(second.registration_date) - new Date(first.registration_date) )
        this.reversedDateSortFlag = true;
        this.switchSort("date");
      } else {
        this.reversedDateSortFlag = false;
        this.sortedUsers.sort((first, second) => new Date(first.registration_date) - new Date(second.registration_date))
        this.switchSort("date");
      }
    },
    sortFromRating() {
      if (!this.reversedRatingSortFlag) {
        this.sortedUsers.sort((first, second) => second.rating - first.rating)
        this.reversedRatingSortFlag = true;
        this.switchSort("rating");
      } else {
        this.reversedRatingSortFlag = false;
        this.sortedUsers.sort((first, second) => first.rating - second.rating)
        this.switchSort("rating");
      }
    },
    switchSort(type) {
      if (type === "date") {
        this.activeSort.date = true;
        this.activeSort.rating = false;
      } else if (type === "rating") {
        this.activeSort.rating = true;
        this.activeSort.date = false;
      }
    },
    clearSortAndFilter(value) {
      if (value) {
        this.sortedUsers = this.users.slice();
        this.activeSort.date = false;
        this.activeSort.rating = false;
      }
    }
  },

}
</script>

<style lang="scss">
#app {
  font-family: Roboto, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  h1 {
    text-align: left;
  }
  .sort-container {
    margin-top: 30px;
    margin-left: 30px;
    text-align: left;
    font-size: 14px ;
    color: grey;
    p {
      display: inline-block;
      border-bottom: 1px dashed #000000;
      cursor: pointer;
      margin-right: 5px;
    }
    .active {
      color: #000000;
      font-weight: bold;
    }
  }
  button {
    cursor: pointer;
  }
  .deleteUser-btn {
    width: 50px;
    height: 30px;
    cursor: pointer;
    background-color: #f80000;
    color: #ffffff;

  }
}
</style>
