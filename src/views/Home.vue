<template>
<div id="home">  
  <Header />
  <v-container class="container-home">
    <h1>Update your activity</h1>
    <v-card
    class="mx-auto"
    max-width="752"
    >
      <v-container>
        <v-textarea
          name="posts"
          label="How about your feelings?"
          v-model="posts"
          hint="Hint text"
        ></v-textarea>
        <div class="btn">
        <v-btn class="btn-cancel">Cancel</v-btn>
        <v-btn class="btn-post">Post</v-btn>
        </div>
      </v-container>
    </v-card>
  </v-container>
</div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import axios from 'axios'
export default {
  name: "Home",
  components: {
    Header,
  },
  data () {
    return {
      user: null,
      posts: ''
    }
  },
  async created() {
    const response = await axios.get('https://wong801-portfolio.herokuapp.com/api/user/getUser', {
      headers: {
        Authorization: 'Bearer' + localStorage.getItem('token')
      }
    })
    this.user = response.data
    console.log(response);
  }
};
</script>
<style lang="scss" scoped>
#home {
  .container-home {
    h1{
      text-align: start;
      margin-bottom: 24px;
    }
    margin: 40px 294px 0px 294px;
    .btn {
      display: flex;
      justify-content: end;
      .btn-cancel {
        text-transform: capitalize;
        margin-right: 10px;
        width: 10vw;
      }
      .btn-post{
        text-transform: capitalize;
        background-color: #04C45C !important;
        color: white; 
        width: 10vw;
      }
    }
  }
}

@media only screen and (max-width: 1280px) {
body {
  width: 65vw;
  height: 65vh; 
  .container-home {
    margin: 40px 0px 0px 0px;
    width: 45vw;
    height: 45vh; 

  }
}
}

@media only screen and (max-width: 960px) {
body {
  .container-home {
    margin: 40px 0px 0px 40px !important;
    width: 90vw;
    height: 90vh; 

  }
}
}
@media only screen and (max-width: 600px) {
body {
  .container-home {
    margin: 40px 0px 0px 5px !important;
    width: 95vw;
    height: 95vh; 

  }
}
}
@media only screen and (max-width: 444px) {
body {
  .container-home {
    margin: 40px 0px 0px 25px !important;
    width: 85vw;
    height: 85vh; 

  }
}
}

</style>
