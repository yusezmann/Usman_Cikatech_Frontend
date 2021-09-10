<template>
  <v-toolbar
  elevation="0"
  class="navbar"
  >
    <v-toolbar-title class="logo">
      Logo
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <div class="user">
      <h5>Joshbar</h5>
      <p>Web Designer</p>
    </div>
    <v-btn class="btn">Logout</v-btn>
  </v-toolbar>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.navbar {
  font-family: Roboto, 'Open Sans', 'Helvetica Neue', 'sans-serif';
    .logo {
    margin-left: 120px;
    font-weight: 900;
    font-size: 26px;
    }
    .user {
    margin-right: 20px;
    h5 {
        font-size: 14px;
        line-height: 20px;
    }
    p {
        font-size: 12px;
        line-height: 16px;
    }
    }
    .btn {
    text-transform: capitalize;
    background-color: #E95750 !important;
    color: white;
    margin-right: 120px;
    }
}
@media only screen and (max-width: 960px) {
  .logo {
    text-align: start;
  }
  .user {
    display: none;
  }
  .btn {
    margin-left: 50px !important;
  }
}
@media only screen and (max-width: 600px) {
  .user {
    display: none;
  }
  .btn {
    margin-left: 50px !important;
  }
}
</style>