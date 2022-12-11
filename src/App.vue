<template>
  <stats-page/>
</template>

<script>
import StatsPage from "@/components/StatsPage";

export default {
  name: 'App',
  components: {
    StatsPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
html,
body {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
  background: linear-gradient(90deg,#392955 0%,#3a6294 100%) fixed;
  color: aliceblue;
  min-height: 100vh;
}
</style>
