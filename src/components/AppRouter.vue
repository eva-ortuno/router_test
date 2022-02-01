<!-- Router.vue -->
<template>
  <component :is="routedComponent"></component>
</template>

<script>
import MainMenu from "./MainMenu";
import Item from "./Item";

const routes = {
  "/": MainMenu,
  "/dashboard-analytics": Item,
  "/reports-analytics": Item,
  "/eigne-reports-analytics": Item,
  "/centricity-analytics": Item,
  "/dashboard-cross-sell": Item,
  "/katalog-cross-sell": Item,
  "/widgets-cross-sell": Item,
  "/kampagnen-cross-sell": Item,
  "/reports-cross-sell": Item
  
};

export default {
  data() {
    return { current: window.location.pathname };
  },
  computed: {
    routedComponent() {
      return routes[this.current];
    }
  }
};
</script>
