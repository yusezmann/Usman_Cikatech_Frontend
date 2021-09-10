<template>
    <v-row>
      <v-col cols="6" >
          <v-img class="img" src="../assets/images/image.jpg" />
      </v-col>
      <v-col>
        <v-row class="register-content">
          <v-col cols="6">
            <v-container class="container">
              <div class="text-title">              
              <p >Get's Started</p><br>
              <h3 >Create your account</h3>
              </div>
              <v-form @submit.prevent="handleSubmit">
                <div>
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
                </div>
                <div class="row">
                  <div class="col-6">
                    <v-subheader class="subheader">
                      First name
                    </v-subheader>
                    <v-text-field
                      v-model="firstName"
                      :error-messages="firstNameErrors"
                      placeholder="First Name"
                      solo
                      required
                      @input="$v.firstName.$touch()"
                      @blur="$v.firstName.$touch()"
                    ></v-text-field>
                  </div>
                  <div class="col-6 ml-4">
                    <v-subheader class="subheader">
                      Last name
                    </v-subheader>
                    <v-text-field
                      v-model="lastName"
                      :error-messages="lastNameErrors"
                      placeholder="Last Name"
                      solo
                      required
                      @input="$v.lastName.$touch()"
                      @blur="$v.lastName.$touch()"
                    ></v-text-field>
                  </div>
                </div>
                <v-subheader class="subheader">
                  Username             
                </v-subheader>
                <v-text-field
                  v-model="username"
                  :error-messages="usernameErrors"
                  placeholder="Username"
                  solo
                  required
                  @input="$v.username.$touch()"
                  @blur="$v.username.$touch()"
                ></v-text-field>
                <v-subheader class="subheader">
                  Password              
                </v-subheader>
                <v-text-field
                  v-model="password"
                  placeholder="Password"
                  type="password"
                  id="password"
                  :error-messages="passwordErrors"
                  solo
                  required
                  @input="$v.password.$touch()"
                  @blur="$v.password.$touch()"
                ></v-text-field>
                <v-subheader class="subheader">
                  Confirm Password             
                </v-subheader>
                <v-text-field
                  v-model="confirmPassword"
                  placeholder="Confirm Password"
                  type="password"
                  :error-messages="confirmPasswordErrors"
                  solo
                  required
                  @input="$v.confirmPassword.$touch()"
                  @blur="$v.confirmPassword.$touch()"
                ></v-text-field>
                <v-btn
                class="btn col-12 mb-4 "
                type="submit"
                @click="submit"
                >
                  Register now
                </v-btn>
                
                
              </v-form>
              <div class="text-login">
              <p>Already have account?<span><router-link to="/login" > Login</router-link></span></p>
              </div>
            </v-container>
          </v-col>
        </v-row>
      </v-col>

    </v-row>
</template>


<script>
import axios from 'axios'
import qs from  'qs'
import { validationMixin } from 'vuelidate'
import { required, email, minLength, sameAs } from 'vuelidate/lib/validators'

  export default {
    name:'Register',
    data () {
      return {        
        email: '',
        firstName: '',
        lastName: '',
        username: '',
        password: '',
        confirmPassword: '',
      }
    },
    mixins: [validationMixin],
    validations: {
      email: { required, email },
      firstName: { required, minLength: minLength(3) },
      lastName: { required, minLength: minLength(3) },
      username: { required, minLength: minLength(3) },
      password: { required, minLength: minLength(6) },
      confirmPassword: { sameAsPassword: sameAs('password') },
    },
    computed: {
      emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Must be valid e-mail')
        !this.$v.email.required && errors.push('E-mail is required')
        return errors
      },
      firstNameErrors () {
        const errors = []
        if (!this.$v.firstName.$dirty) return errors
        !this.$v.firstName.minLength && errors.push('First Name must be at least 3 characters long')
        !this.$v.firstName.required && errors.push('First Name is required.')
        return errors
      },
      lastNameErrors () {
        const errors = []
        if (!this.$v.lastName.$dirty) return errors
        !this.$v.lastName.minLength && errors.push('Last Name must be at least 3 characters long')
        !this.$v.lastName.required && errors.push('Last Name is required.')
        return errors
      },
      usernameErrors () {
        const errors = []
        if (!this.$v.username.$dirty) return errors
        !this.$v.username.minLength && errors.push('User Name must be at least 3 characters long')
        !this.$v.username.required && errors.push('User Name is required.')
        return errors
      },
      passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.minLength && errors.push('Password must be at least 6 characters ')
        !this.$v.password.required && errors.push('Password is required.')
        return errors
      },
      confirmPasswordErrors () {
        const errors = []
        if (!this.$v.confirmPassword.$dirty) return errors
        !this.$v.confirmPassword.sameAsPassword && errors.push('Password must be matching.')
        return errors
      },
      
    },

    methods: {
      async handleSubmit () {
        // set url
        const url =' https://wong801-portfolio.herokuapp.com/api/user/register'

        // set header
          const config = {
              headers: {
                'content-type': 'application/x-www-form-urlencoded'
              },
          }
        
        // const response = 
        await axios.post(url, qs.stringify({
          email: this.email,
          firstName: this.firstName,
          lastName: this.lastName,
          username: this.username,
          password: this.password,
          confirmPassword: this.confirmPassword
        }),config)

        this.$router.push('/login')
        // console.log(response);
      },
      submit () {
        this.$v.$touch()
      },
      clear () {
        this.$v.$reset()
        this.email = ''
        this.firstName = ''
        this.lastName = ''
        this.username = ''
        this.password = ''
        this.confirmPassword = ''
      },
    },
  }
</script>
<style lang="scss" scoped>
.register-content {  
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
    margin-top: 50px;
    .text-title {
      text-align: start;
      p {
        font-size: 16px;
      }
      h3 {
        font-size: 25px;
      }
    }
  }
  .subheader {
    margin-left:-20px;
  }
  .btn {
    text-transform:capitalize;
    background-color: #04C45C !important;
    color: white;
  }
  .text-login {
    margin-top:20px;
    a {
      text-decoration:none;
    }
  }
}


@media only screen and (max-width: 1280px) {
  /* For desktop: */
.register-content {
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
  .register-content {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin-right: 70px;
    .container {
      width: 65vw;
      height: 65vh;
      margin-bottom: 10px;        
      margin-top: 5px;
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
@media only screen and (max-width: 600px) {
  /* For desktop: */
.register-content {
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
  
.register-content {
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

