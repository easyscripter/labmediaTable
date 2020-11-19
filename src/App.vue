<template>
  <div id="app">
    <h1>Список пользователей</h1>
    <table-component columnsName="Имя пользователя, E-mail, Дата регистрации, Рейтинг"/>
  </div>
</template>

<script>
import tableComponent from "@/components/table-component"
export default {
  name: 'App',
  components: {
    tableComponent
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
