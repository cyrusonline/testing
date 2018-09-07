<template>
  <!-- App -->
  <div id="app">

    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>

    <!-- Left Panel / View -->
    <left-panel-view />

    <!-- Main View -->
    <f7-view id="main-view" url="/" main></f7-view>


  </div>
</template>

<script>
import LeftPanel from './components/LeftPanel';
import firebase from 'firebase';
 var config = {
    apiKey: "AIzaSyBFmys2X9eU-VUzJ75B2VpIW41YJaEkmmI",
    authDomain: "yrmentor2018.firebaseapp.com",
    databaseURL: "https://yrmentor2018.firebaseio.com",
    projectId: "yrmentor2018",
    storageBucket: "yrmentor2018.appspot.com",
    messagingSenderId: "176560638600"
  };
  firebase.initializeApp(config);
  firebase.firestore().settings({
  timestampsInSnapshots: true
})


export default {
  name: 'App',
  components: {
    'left-panel-view': LeftPanel
  },
  methods: {
    handleBackButton() {
      // NOTE: The back button will behave differently depending on circumstance
      // If the side panel is open, close it
      if (document.querySelector('.panel-left.panel-active')) {
        // This will do nothing when the split-view is open
        return this.$f7.panel.close();
      }
      // Close modals
      // @TODO How to handle modals we shouldn't close like a login-screen?
      if (document.querySelector('.modal-in')) {
        return this.$f7.popover.close();
      }
      // If we have a back button, we want it to go back
      if (this.$f7.views.main.router.history.length > 1) {
        return this.$f7.views.main.router.back();
      }
      // Default to closing the app
      return window.navigator.app.exitApp();
    }
  },
  computed: {
    isiOS() {
      return this.$theme.ios;
    }
  },
  created() {
    document.addEventListener('backbutton', this.handleBackButton);
  }
};
</script>

<style>
/* style is not `scoped` so navbars in Pages are modified as well */
@media (min-width: 960px) {
  /* Let's hide panel-opener button when left panel is visible */
  .view-main .navbar .panel-open {
    display: none;
  }
}
</style>
