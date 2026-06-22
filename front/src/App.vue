<template>
  <div id="app">
    <header>
      <router-link to="/">DevOps Student Directory</router-link>
    </header>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App"
};
</script>

<style>
body {
  margin: 0;
  background: #f5f7fa;
}

#app {
  min-height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

header {
  margin-bottom: 40px;
  padding: 24px;
  background: #17365d;
}

header a {
  color: white;
  font-size: 24px;
  font-weight: 600;
}
</style>
