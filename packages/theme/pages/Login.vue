<template>
  <div>
    <div class="top-bar">
      <div @click="goBack" class="sf-chevron--left sf-chevron icon_back">
        <span class="sf-search-bar__icon">
          <SfIcon color="var(--c-primary)" size="20px" icon="chevron_left" />
        </span>
      </div>
      <div class="header-push">Sign in</div>
    </div>
    <div class="open-search">
      <h3>
        Open <br />
        Commerce
      </h3>
      <h4>for All</h4>
      <div class="traditional-login-container" style="width: 60%;">
          <SfInput v-model="loginEsmail" :type="'text'" :label="'Email*'" />
          <SfInput label="Password*" type="password"
            :icon='{"icon":"show_password","color":"black","size":"18px"}' valid hasShowPassword />
          <SfButton type="button" @click="userSignIn">Sign In</SfButton>
      </div>
    </div>
    <div></div>
  </div>
</template>

<script>
import { SfButton, SfIcon, SfInput } from '@storefront-ui/vue';
// import {state} from '../store/index.js'

export default {
  middleware: 'auth',
  name: 'Login',
  components: {
    SfIcon,
    SfButton,
    SfInput
  },
  setup(_, context) {
    const goBack = () => context.root.$router.back();
    return {
      goBack
    };
  },
  data() {
    return {
      loginEsmail: '',
      showPwd: true
    };
  },
  methods: {
    userSignIn() {
      // function ValidateEmail(mail) {
      /* eslint-disable */
        if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.loginEsmail)) {
        alert('User Signed In successful !');
        } else {
        // }
        alert("Incorrect email id patern")
        }
        /* eslint-enable */
    },
    facebookLogin() {
      /* eslint-disable no-undef */

      const provider = new $nuxt.$fireModule.auth.FacebookAuthProvider();
      provider.addScope('email');
      this.$fire.auth
        .signInWithPopup(provider)
        .catch((error) => {
          this.snackbarText = error.message;
          this.snackbar = true;
        })
        .then(() => {
          // we are signed in
          $nuxt.$router.push('/');
        });
    },
    googleLogin() {
      /* eslint-disable no-undef */
      const provider = new $nuxt.$fireModule.auth.GoogleAuthProvider();
      provider.addScope('email');
      this.$fire.auth
        .signInWithPopup(provider)
        .catch((error) => {
          this.snackbarText = error.message;
          this.snackbar = true;
        })
        .then(() => {
          // we are signed in
          // console.log("STATE1",state)
          $nuxt.$router.push('/');
        });
    }
  }
};
</script>

<style lang="scss" scoped>
  .top-bar {
    align-items: center;
    display: flex;
    font-size: 18px;
    justify-content: space-around;
    height: 60px;
    font-weight: 500;
    background: white;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.07);

    .icon_back {
      position: absolute;
      left: 0;
      margin: 10px;
    }
  }

  .open-search {
    @media (min-width: 560px) {
      padding-top: 40px;
      width: 50%;
      margin: auto;
    }

    padding: 40px 28px;

    h3 {
      font-size: 40px;
      font-weight: 800;
      color: #f37a20;
      line-height: 45px;
    }

    h4 {
      font-size: 27px;
      font-weight: 800;
      line-height: 30px;
    }

    .socialMedia-login-container {
      padding-top: 41px;
    }

    .span-text {
      padding-right: 225px;
    }

    .social-span-content {
      position: absolute;
    }

    .google-button {
      width: 300px;
      text-transform: capitalize;
      border-radius: 6px;
      background: #5383ec;
    }

    .facebook-button {
      width: 300px;
      margin-top: 30px;
      text-transform: capitalize;
      border-radius: 6px;
      background: #4a66ac;
    }
  }
</style>
