<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto');
:root{
  --mainBgColor: #9B30FF;
  --mainAccentColor: #deff30;
  --mainFontColor: #f8f8ff;
}
html, body {
  margin: 0;
  padding: 0;
  font-size: 12px;
}
#app {
  margin: 0;
  padding: 0;
  height: 100vh;
  font-family: 'Roboto', sans-serif;
  word-spacing: 0.1rem;
  letter-spacing: 0.09rem;
  text-align: center;
  background-color: var(--mainBgColor);
  color: #f8f8ff;
}

h1{
  margin: 0;
  padding: 0;
}
</style>
