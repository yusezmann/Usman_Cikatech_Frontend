<template>
    <v-row>
      <v-col cols="6">
        <v-img class="img d-none d-sm-flex" src="../assets/images/image.jpg" />
      </v-col>
      <v-col>
        <v-row class="login-content">
          <v-col cols="6">
          <v-container class="container">
              <div class="text-title">              
              <p >Welcome back</p><br>
              <h3 >Login to your account</h3>
              </div>
            <v-form @submit.prevent="handleSubmit">
              <v-subheader class="subheader">
                Email              
              </v-subheader>
              <v-text-field
              v-model="email"
              :error-messages="emailErrors"
              placeholder="E-mail"
              solo
              required
              @input="$v.email.$touch()"
              @blur="$v.email.$touch()"
              ></v-text-field>
              <v-subheader class="subheader">
                Password              
              </v-subheader>
              <v-text-field
              v-model="password"
              :error-messages="passwordErrors"
              placeholder="Password"
              type="password"
              solo
              required
              @input="$v.password.$touch()"
              @blur="$v.password.$touch()"
              ></v-text-field>
              <div class="row radio-button ">
                <div class="col">                        
                <v-radio
                v-model="radiobutton"
                label="Remember me"
                :error-messages="radioButtonErrors"
                value="checked"
                required
                @change="$v.radiobutton.$touch()"
                @blur="$v.radiobutton.$touch()"
                ></v-radio>
                </div>
                <div class="col">                        
                <a class="forgot" href="#" > Forgot password?</a>
                </div>
              </div>
              <v-btn
              class="btn col-12 mb-4 "
              type="submit" @click="submit"
              >
                Login now
              </v-btn> 
            </v-form>
            <div style="margin-top:20px;">
            <p>Don't have an account?<span><router-link to="/register" style="text-decoration:none;" > Register</router-link></span></p>
            </div>
          </v-container>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
</template>


<script>
import { validationMixin } from 'vuelidate'
import { required, maxLength, email } from 'vuelidate/lib/validators'
import axios from 'axios'
  export default {
    name:'Login',
    data () {
      return { 
        email: '',
        password: '',
        radiobutton: false,
      }
    },
    mixins: [validationMixin],

    validations: {
      email: { required, email },
      password: { required, maxLength: maxLength(16) },
      radiobutton: {
        checked (val) {
          return val
        },
      },
    },

    computed: {
      radioButtonErrors () {
        const errors = []
        if (!this.$v.radiobutton.$dirty) return errors
        !this.$v.radiobutton.checked && errors.push('You must agree to continue!')
        return errors
      },
      passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.maxLength && errors.push('Password must be at most 10 characters long')
        !this.$v.password.required && errors.push('Password is required.')
        return errors
      },
      emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Must be valid e-mail')
        !this.$v.email.required && errors.push('E-mail is required')
        return errors
      },
    },

    methods: {
      submit () {
        this.$v.$touch()
      },
      clear () {
        this.$v.$reset()
        this.email = ''
        this.password = ''
        this.radiobutton = false
      },
      async handleSubmit () {
        const url ='https://wong801-portfolio.herokuapp.com/api/user/login'
        const response = await axios.post(url, {
          username: this.email,
          password: this.password
        })
        localStorage.setItem('token', response.data.token)
        this.$router.push('/')
        // console.log(response.data.token);
      }
    },
  }
</script>

<style lang="scss" scoped>

.login-content{
  font-family: Roboto, 'Open Sans', 'Helvetica Neue', 'sans-serif';
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
  .img {
    width:720px;
    height:899px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
  .container{
    width: 25vw;
    height: 25vh;
    margin-top: 120px;
    .text-title {
      text-align: start;
      p {
        font-size: 16px;
      }
      h3 {
        font-size: 25px;
      }
    }
    
    .subheader {
      margin-left:-20px;
    }
    .radio-button {
      margin-bottom:20px;
      .forgot {
        text-decoration:none;
      }
    }
    .btn {
      text-transform:capitalize;
      background-color: #04C45C !important;
      color: white;
    }
  }
}

@media only screen and (max-width: 1280px) {
  /* For desktop: */
.login-content {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-right: 50px;
  .container {
    width: 35vw;
    height: 35vh;
    .text-title {
        p {
          font-size: 16px;
        }
        h3 {
          font-size: 25px;
        }
      }
    }
  }
}

@media only screen and (max-width: 960px) {
  /* For tablets: */
  .img {
    display: none;
  }
  .login-content {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin-right: 70px;
    .container {
      width: 65vw;
      height: 65vh;
      margin-bottom: 10px;
    // display: grid;
        
      .text-title {
        margin-top: 5px;
        p {
          font-size: 16px;
        }
        h3 {
          font-size: 25px;
        }
      }
    }
  }
}
@media only screen and (max-width: 600px) {
  /* For desktop: */
.login-content {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-right: 125px;
  .container {
    width: 65vw;
    height: 65vh;
    .text-title {
      margin-top: 5px;
        p {
          font-size: 16px;
        }
        h3 {
          font-size: 25px;
        }
      }
    }
  }
}
@media only screen and (max-width: 444px) {
  
.login-content {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  // margin-right: 125px;
  .container {
    width: 65vw;
    height: 65vh;
    .text-title {
      margin-top: 5px;
        p {
          font-size: 16px;
        }
        h3 {
          font-size: 25px;
        }
      }
    }
  }
}
</style>
