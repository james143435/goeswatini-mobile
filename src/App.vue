<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>GOEswatini Management</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat @click="create_dialog=true" target="_blank">
        <span class="mr-2">New Spot</span>
      </v-btn>
    </v-toolbar>
    <v-content>
      <newspot :dialog="create_dialog" @close="create_dialog=false" @save="save">
        <GmapMap
          :center="{lat:-26.489286331271874, lng:31.34843022086102}"
          :zoom="7"
          map-type-id="hybrid"
          @click="mapclick"
          style="width: 500px; height: 300px"
        ></GmapMap>
        Latitude: {{lat}} , Longitude: {{lng}}
      </newspot>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import newspot from "./components/newspot";
import firebase from "firebase";

const config = {
  apiKey: "AIzaSyDqe-35kl9BwmbTrwISfwA5EUdUcUtl18E",
  authDomain: "goeswatini.firebaseapp.com",
  databaseURL: "https://goeswatini.firebaseio.com",
  projectId: "goeswatini",
  storageBucket: "goeswatini.appspot.com",
  messagingSenderId: "817655537607"
};

firebase.initializeApp(config);
//storage = firebase.storage();
let db = firebase.firestore();

export default {
  name: "App",
  components: {
    newspot
  },
  data() {
    return {
      create_dialog: false,
      lat: 0,
      lng: 0
    };
  },
  methods: {
    save(data) {
     this.create_dialog = false
      db.collection("aoi")
        .add({ ...data, location: { lat: this.lat, lng: this.lng } })
        .then(function(docRef) {
          console.log("Document written with ID: ", docRef.id);
        })
        .catch(function(error) {
          console.error("Error adding document: ", error);
        });
    },
    mapclick(a, b, c) {
      console.log(a.latLng.lat(), a.latLng.lng());
      this.lat = a.latLng.lat();
      this.lng = a.latLng.lng();
    }
  }
};
</script>
