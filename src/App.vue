<template>
  <div id = "app">
    <AppHeader/>
    <AppTodos/>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader";
import AppTodos from "./components/AppTodos";
export default {
  name: "App",
  components: {
    AppHeader, AppTodos
  }
}
</script>

<style>
#app {
font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
</style>