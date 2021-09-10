<template>
  <div id="app">
    <!-- <Header /> -->
    <router-view />
  </div>
</template>

<script>
// @ is an alias to /src
// import Header from "@/components/Header.vue";

export default {
  name: "Home",
  // components: {
  //   Header,
  // },
};
</script>
<style lang="scss" scoped>
#app{
  
  background-color: #E5E5E5;
  font-family: Roboto, 'Open Sans', 'Helvetica Neue', 'sans-serif';
}

</style>
