<template>
  <FormComp @Theme="handleThemeColor()" />
</template>

<script setup>
// const bodyElem = document.body;

function handleThemeColor() {
  console.log("Theme");
  let red = Math.floor((Math.random() * 1000) % 256);
  let green = Math.floor((Math.random() * 1000) % 256);
  let blue = Math.floor((Math.random() * 1000) % 256);

  document.body.style.backgroundColor = `rgb(${red},${green},${blue})`;
}

// document.documentElement.addEventListener("keyup", function (e) {
//   console.log(e.code);
//   if (e.code === "Space") {
//     handleThemeColor();
//   }
// });
</script>

<script>
import FormComp from "./components/FormComp.vue";

export default {
  name: "App",
  components: { FormComp },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
