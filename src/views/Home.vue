<template>
  <div class="page-wrapper">
    <div class="page-header">
      <img class="ping-logo" src="@/assets/img/logo.svg" alt="Ping.">
      <h1 class="page-title">We are launching <span>soon!</span></h1>
      <p class="subtitle">Subscribe and get notified</p>
    </div>

    <form class="ping-form" action="#" method="post">
      <div class="input-wrapper">
        <input
          class="email-validator"
          :class="{ 'is-error': invalidForm }"
          v-model="email"
          type="email"
          name="email"
          placeholder="Your email address..."
        />

        <p v-if="invalidForm" class="error-message">
          Please provide a valid email address
        </p>
      </div>
      <button type="submit" @click="validateForm">Notify Me</button>
    </form>

    <img class="dashboard-img" src="@/assets/img/illustration-dashboard.png" alt="Dashboard" />

    <div class="socials-wrapper">
      <a class="social-btn facebook" href="#">
        <i class="icon-facebook"></i>
      </a>
      <a class="social-btn twitter" href="#">
        <i class="icon-twitter"></i>
      </a>
      <a class="social-btn instagram" href="#">
        <i class="icon-instagram"></i>
      </a>
    </div>
    <p class="copyright-text">&copy; Copyright Ping. All rights reserved.</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data() {
    return {
      invalidForm: false,
      email: '',
    }
  },
  head() {
    return {
      title: {
        inner: 'Home'
      },
      meta: [
        {
          name: 'description',
          content: `${this.appTitle} home page`,
          id: 'desc'
        }
      ]
    }
  },
  mounted() {
  },
  methods: {
    validateForm(e) {
      e.preventDefault()

      const emailRegex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

      const emailState = emailRegex.test(String(this.email).toLowerCase())

      this.invalidForm = !emailState

      return false
    }
  },
  computed: mapState('app', ['appTitle'])
}
</script>

<style lang="scss" scoped>
@import '@/theme/variables.scss';

.page-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;

  .page-header {
    margin-bottom: 40px;

    @media (max-width: 600px) {
      margin-bottom: 32px;
    }

    .page-title {
      margin: 40px 0 16px;
      font-weight: 300;
      font-size: 48px;
      line-height: 60px;
      color: $neutralColor1;

      @media (max-width: 600px) {
        margin: 32px 0 15px;
        font-size: 22px;
        line-height: 32px;
      }

      span {
        color: $neutralColor2;
        font-weight: 700;
      }
    }
  }

  .ping-form {
    display: flex;
    align-items: flex-start;
    width: 100%;

    @media (max-width: 600px) {
      flex-direction: column;
    }

    .input-wrapper {
      display: flex;
      flex-direction: column;
      width: 100%;

      @media (max-width: 600px) {
        margin-bottom: 20px;
      }

      input {
        width: 100%;
        padding: 18px 30px;
        background: $light;
        border: 1px solid $secondaryColor1;
        box-sizing: border-box;
        box-shadow: 0 0 7px 3px rgba(0, 0, 0, 0.0001);
        border-radius: 28px;
        font-weight: 300;
        font-size: 16px;
        line-height: 20px;
        outline: 0;
        color: $neutralColor2;

        @media (max-width: 600px) {
          padding: 10px 32px;
          font-size: 12px;
        }

        &::placeholder {
          color: $secondaryColor1;
        }

        &.is-error {
          border-color: $secondaryColor2;
        }
      }

      .error-message {
        margin: 6px 0 0 30px;
        text-align: left;
        font-style: italic;
        font-weight: normal;
        font-size: 12px;
        line-height: 20px;
        letter-spacing: 0.15px;
        color: $secondaryColor2;

        @media (max-width: 600px) {
          margin-left: 0;
          font-size: 10px;
          text-align: center;
        }
      }
    }

    button {
      width: 200px;
      flex: 1 0 auto;
      padding: 19px 0;
      margin-left: 16px;
      background: $primaryColor;
      box-shadow: 0 5px 10px 2px rgba(76, 123, 243, 0.230414);
      border: none;
      border-radius: 28px;
      font-weight: 600;
      font-size: 16px;
      line-height: 19px;
      text-align: center;
      color: $light;
      transition: background-color .3s ease-in-out;
      cursor: pointer;

      @media (max-width: 600px) {
        padding: 12px 0;
        margin-left: 0;
        font-size: 12px;
        line-height: 16px;
        width: 100%;
      }

      &:hover {
        background: rgba($primaryColor, .8);
        mix-blend-mode: normal;
      }
    }
  }

  .dashboard-img {
    max-width: 100%;
    margin: 94px auto 72px;

    @media (max-width: 767px) {
      margin: 40px 0;
    }
  }

  .socials-wrapper {
    display: flex;
    align-items: center;
    margin-bottom: 25px;

    .social-btn {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 31px;
      height: 31px;
      border-radius: 50%;
      border: 1px solid rgba($primaryColor, 0.15);
      transition: background .3s ease-in-out;

      &:not(:last-child) {
        margin-right: 13px;
      }

      &:hover {
        background-color: $primaryColor;

        i {
          color: $light;
        }
      }

      i {
        color: $primaryColor;
        transition: color .3s ease-in-out;
      }
    }
  }

  .copyright-text {
    font-weight: 300;
    font-size: 12px;
    line-height: 15px;
    color: $neutralColor1;

    @media (max-width: 767px) {
      font-size: 10px;
    }
  }
}

[class^="icon-"], [class*=" icon-"] {
  /* use !important to prevent issues with browser extensions that change fonts */
  font-family: 'icomoon' !important;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-facebook:before {
  content: "\ea90";
}
.icon-instagram:before {
  content: "\ea92";
}
.icon-twitter:before {
  content: "\ea96";
}
</style>
