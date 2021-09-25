<template>
  <div id="app">
    <div class="main-wrapper">
      <router-view />
    </div>

    <new-content-available-toastr
      v-if="newContentAvailable"
      class="new-content-available-toastr"
      :refreshing-app="refreshingApp"
      @refresh="serviceWorkerSkipWaiting"
    ></new-content-available-toastr>
    <apple-add-to-home-screen-modal
      v-if="showAddToHomeScreenModalForApple"
      class="apple-add-to-home-screen-modal"
      @close="closeAddToHomeScreenModalForApple(false)"
    >
    </apple-add-to-home-screen-modal>
  </div>
</template>
<script>
import NewContentAvailableToastr from '@/components/NewContentAvailableToastr'
import AppleAddToHomeScreenModal from '@/components/AppleAddToHomeScreenModal'
import { mapState, mapActions, mapGetters } from 'vuex'

export default {
  components: { NewContentAvailableToastr, AppleAddToHomeScreenModal },
  computed: {
    ...mapGetters('app', ['newContentAvailable']),
    ...mapState('app', ['showAddToHomeScreenModalForApple', 'refreshingApp'])
  },
  methods: mapActions('app', [
    'closeAddToHomeScreenModalForApple',
    'serviceWorkerSkipWaiting'
  ])
}
</script>

<style lang="scss">
@import '@/theme/variables.scss';

body {
  margin: 0;

  a {
    font-weight: 500;
    text-decoration: none;
  }

  * {
    box-sizing: border-box;
  }

  h1,
  p {
    font-family: $textFont;
    margin: 0;
  }

  p {
    font-size: 20px;
    line-height: 24px;
    color: $neutralColor2;

    @media (max-width: 767px) {
      font-size: 12px;
      line-height: 15px;
    }
  }

  #app {
    font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
      Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 16px;
    color: #2c3e50;

    .new-content-available-toastr {
      position: absolute;
      bottom: 10px;
      right: 10px;
    }

    .main-wrapper {
      display: flex;
      height: 100%;
      width: 100%;
      padding: 80px 40px 40px;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background: $light;

      .page-wrapper {
        width: 100%;
        max-width: 640px;
        margin: auto;
      }
    }
  }
}
</style>
