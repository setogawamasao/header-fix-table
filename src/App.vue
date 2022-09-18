<template>
  <div id="app">
    <!-- <HelloWorld /> -->
    <!-- <br /><br /><br /> -->
    <HelloWorld2 />
    <br /><br /><br />
    <HelloWorld3 />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import HelloWorld2 from "./components/HelloWorld2.vue";
import HelloWorld3 from "./components/HelloWorld3.vue";

export default {
  name: "app",
  components: {
    // HelloWorld,
    HelloWorld2,
    HelloWorld3,
  },
};
</script>
