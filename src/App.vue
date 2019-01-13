<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { components } from "aws-amplify-vue";
export default {
  name: "app",
  components: {
    ...components,
    HelloWorld
  }
};
</script>

<style>
</style>
