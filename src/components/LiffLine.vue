<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="profile.pictureUrl"
          class="my-3"
          contain
          height="200"
        />
      </v-col>
      <v-col cols="12">
        <h3>ข้อมูลจาก Get Profile</h3>
      </v-col>
      <v-col cols="12">
        <v-text-field
          label="ชื่อ Line"
          v-model="profile.displayName"
        ></v-text-field>
      </v-col>
      <v-col cols="12">
        <v-text-field
          label="Liff UserId"
          v-model="profile.userId"
        ></v-text-field>
      </v-col>
    </v-row>
  </v-container>
 </template>

<script>
  export default {
    data: () => ({
      profile: null,
      pictureUrl: '',
      displayName: '',
      userId: '',
    }),

    mounted () {
      this.checkLiffLogin()
      // this.getProfile()
    },
    methods: {
      async checkLiffLogin () {
       await this.$liff
         .init({
           liffId: '2003875538-7xkdXv30'  // นำ liffId มาจาก liff ที่เราสร้างตอนแรก
         })
         .then(async () => {
             if (!this.$liff.isLoggedIn()) { // check ว่าได้ ถ้ายังไม่ได้ Login จะพาไป Login ก่อนแล้วจะนำกลับมาหน้า ปัจจุบัน
               this.$liff.login({ redirectUri: window.location.href })
             } else {
               await this.getProfile() // Login แล้วจะนำไป Functions getProfile
             }
         })
         .catch(err => {
           console.log(err.code, err.message)
         })
     },
     async getProfile () {
       let _this = this
       await this.$liff
         .getProfile()
         .then(function (profile) {
           _this.profile = profile
           console.log('prod', _this.profile)
         })
         .catch(function (error) {
           console.log('Error getting profile: ' + error)
         })
     },
    }
  }
</script>
