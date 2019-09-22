<template>
  <div id="app">
    <app-header />
  </div>
</template>

<script>
import "@/assets/styles.scss";
import Header from "@/components/Header";

export default {
  name: "app",
  components: { appHeader: Header }
};
</script>
