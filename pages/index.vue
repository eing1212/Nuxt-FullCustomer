<template>
  <div class="login100">
      <v-card class="wrap-login100" color="rgba(255, 255, 255, 0.75)">
        <v-row class="center"
          ><v-col cols="6">
            <v-img
              src="https://illustoon.com/photo/1774.png"
            ></v-img
          ></v-col>
          <v-col cols="6">
            <v-container>
              <v-form>
                <v-row>
                  <v-col cols="12">
                    <h1 class="logtitle">Owner Sign in</h1>
                    <v-text-field
                      v-model="email"
                      label="E-mail"
                      required
                      filled
                      rounded
                      dense
                      solo-inverted
                      :rules="emailRules"
                    ></v-text-field
                  ></v-col>
                  <v-col cols="12">
                    <v-text-field
                      v-model="password"
                      :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
                      :type="show2 ? 'text' : 'password'"
                      :rules="[rules.required, rules.min]"
                      name="input-10-2"
                      label="Password"
                      class="input-group--focused"
                      filled
                      rounded
                      dense
                      solo-inverted
                      @click:append="show2 = !show2"
                    ></v-text-field></v-col
                ></v-row>
                <v-hover>
                  <v-btn
                    rounded
                    class="container-btn"
                    color="#DCB13C"
                    @click="login()"
                  >
                    SIGN IN
                  </v-btn></v-hover
                >
              </v-form>
            </v-container>
          </v-col>
        </v-row>
      </v-card>
    </div>
</template>

<script>
import firebase from 'firebase/app'
import { auth } from '~/plugins/firebaseConfig.js'
export default {
  layout: 'login',
  //   layout: 'loginGoogle',
  data() {
    return {
      show2: false,
      email: '',
      password: '',
      clock: {
        el: '#clock',
        data: {
          time: '',
          date: '',
        },
      },
      emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ],
      show1: false,
      rules: {
      required: value => !!value || 'Required.',
      min: v => v.length >= 8 || 'Min 8 characters'
      },
    }
  },
  methods: {
    checkUser() {
      var user = auth.currentUser
      console.log(user === null)
    },
    // logout() {
    //   auth
    //     .signOut()
    //     .then(() => {
    //       // Sign-out successful.
    //       console.log('Sign-out successful')
    //     })
    //     .catch((error) => {
    //       // An error happened.
    //       console.log(error)
    //     })
    // },
    login() {
      auth
        .signInWithEmailAndPassword(this.email, this.password)
        .then((result) => {
          // This gives you a Google Access Token. You can use it to access the Google API.
          const token = result.credential
          // The signed-in user info.
          const user = result.user
          console.log('token x : ' + token)
          console.log('user x : ' + user)
         if (user.email == 'owner@gmail.com') {
            this.$router.replace('/ShopCustomer')
            alert('login successful!')
          } else {
          this.$router.replace('/')
           alert('Email or Password uncorrect!')
          }
        })

        .catch((error) => {
          // Handle Errors here.
          const errorCode = error.code
          const errorMessage = error.message
          console.log('ErrorCode' + errorCode)
          alert('Email or Password uncorrect!')
          console.log('ErrorCode' + errorMessage)
          // ...
        })
    },
  },
  computed: {
    index() {
      return this.$router.replace('/')
    },
  },
}
</script>
<style>
.sp {
  margin-top: 1rem;
}
.container-btn {
  width: 100%;
  display: -webkit-box;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding-top: 10px;
}
.logtitle {
  color: #333333;
  line-height: 1.2;
  text-align: center;
  width: 100%;
  display: block;
  padding-bottom: 54px;
}
.wrap-login100 {
  width: 960px;
  border-radius: 20px;
  overflow: hidden;
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 50px 50px 50px 95px;
}
.login100 {
  width: 100%;
  min-height: 100vh;
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: -webkit-linear-gradient(-135deg, #df67d5, #d352c8);
  background: -o-linear-gradient(-135deg, #ea53f0, #ec63c3);
  background: -moz-linear-gradient(-135deg, #f36ef3, #e65ace);
  background: linear-gradient(-135deg, #d351d8, #ff69eb);
}
</style>
