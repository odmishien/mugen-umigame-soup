<template>
  <div>
    <Title />
    <Soup />
  </div>
</template>

<script>
import Title from "./components/Title";
import Soup from "./components/Soup";
export default {
  name: "App",
  components: {
    Title,
    Soup,
  }
};
</script>

<style>
  input {
    font-size: 16px;
  }
</style>
