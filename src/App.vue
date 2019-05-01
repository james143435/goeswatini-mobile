<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat @click="create_dialog=true" target="_blank">
        <span class="mr-2" >New Spot</span>
      </v-btn>
    </v-toolbar>
    <v-content>
      <newspot :dialog="create_dialog" @close="create_dialog=false" @save="save">
        
      </newspot>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import newspot from "./components/newspot";
import firebase from 'firebase'

  var config = {
    apiKey: "AIzaSyDqe-35kl9BwmbTrwISfwA5EUdUcUtl18E",
    authDomain: "goeswatini.firebaseapp.com",
    databaseURL: "https://goeswatini.firebaseio.com",
    projectId: "goeswatini",
    storageBucket: "goeswatini.appspot.com",
    messagingSenderId: "817655537607"
  };
  
  firebase.initializeApp(config);
  var storage = firebase.storage();

export default {
  name: "App",
  components: {
    HelloWorld,
    newspot
  },
  data() {
    return {
      create_dialog: false
    };
  },
  methods: {
    save() {}
  }
};
</script>
