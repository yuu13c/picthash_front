<template>
  <v-container fluid>
    <v-row justify="center">
      <v-col cols=12 xs="12" md="12">
        <p class="text-center display-2">#> PictHash</p>
        <br>
        <p class="text-center">
          PictHashは、誰でも簡単に画像からハッシュ値を取得できるWebサービスです。<br>
          ある画像を探す時や、他の画像とどのくらい似ているかを調べる時などにご利用下さい！
        </p>
        <br>
      </v-col>
    </v-row>

    <v-row justify="center">
      <!-- File upload area -->
      <v-col cols=12 xs="3" sm="6" md="6">
        <v-file-input
          :rules="rules"
          @change="getFileName"
          accept="image/*"
          label="Select your image"
          outlined
          dense
        />
      </v-col>
      <!-- Create hash value button -->
      <v-col cols="auto">
        <v-btn
          @click="outDigest"
          color="blue darken-1"
          depressed
          dark
          :loading="loading"
          :disable="loading"
        >
          <v-icon>mdi-shuffle-variant</v-icon>
        </v-btn>
      </v-col>
    </v-row>

    <v-row justify="center">
      <!-- Hash value output area -->
      <v-col cols=12 xs="3" sm="6" md="6">
        <span class="title grey--text text--darken-3">#> <span class="headline font-weight-light grey--text text--darken-3">{{digest}}</span></span>
      </v-col>
    </v-row>

    <v-row justify="center">
      <v-col cols=12 xs="3" sm="6" md="6">
        <div v-if="alert">
          <v-alert class="font-weight-medium" dense type="error">入力内容を確認して下さい</v-alert>
        </div>
      </v-col>
    </v-row>

    <Description/>

  </v-container>
</template>

<script>
import firebase from 'firebase'
import axios from 'axios'
import Description from '@/components/Description.vue'

export default {
  name: 'Home',
  components: {
    Description,
  },
  data () {
    return {
      loading: false,
      digest: null,
      file: null,
      imageURL: null,
      rules: [
        v => !!v || 'Image file is required',
      ],
      alert: false,
    }
  },
  methods: {
    getFileName: function (event) {
      this.file = event
      this.alert = false
    },
    outDigest: function () {
      try {
        const endPoint = 'https://picthash-backend.herokuapp.com/digest'
        
        var uniqueName = Math.random().toString(32).substring(2)
        var mountPoint = 'tmp/' + this.file.name + '_' + uniqueName
        var storageRef = firebase.storage().ref()
        var mountainsRef = storageRef.child(mountPoint)
  
        this.loading = true
        mountainsRef.put(this.file).then(snapshop => {
          snapshop.ref.getDownloadURL().then(downloadURL => {
            this.imageURL = downloadURL
            axios({
              method: 'POST',
              url: endPoint,
              data: { 'url':this.imageURL }
            }).then(respons => {
              const data = respons.data
              this.digest = data['digest']
              mountainsRef.delete()
              this.loading = false
            })
          })
        })
      } catch (error) {
        this.alert = true
      }
    }
  }
}
</script>