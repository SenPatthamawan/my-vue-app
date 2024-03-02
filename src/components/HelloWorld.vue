<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          ข้อมูลส่วนตัว
        </h1>

        <v-text-field
            v-model="name"
            :rules="nameRules"
            :counter="10"
            label="ชื่อ"
            required
          ></v-text-field>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <v-text-field
            v-model="age"
            :rules="ageRules"
            :counter="2"
            label="อายุ"
            required
          ></v-text-field>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <v-checkbox
          v-model="maritalStatus"
          label="สถานภาพสมรส"
        ></v-checkbox>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <v-checkbox
          v-model="test"
          label="test"
        ></v-checkbox>
      </v-col>

      <v-col cols="12" v-for="item,index in dataList" :key="index">
        <div v-if="item.text !== 'test2'">{{ item.text }}</div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      valid: false,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      age: '',
      ageRules: [
        v => !!v || 'Name is required',
        v => v.length <= 2 || 'Name must be less than 2 characters',
      ],
      maritalStatus: false,
      dataList: [
        {text: 'test1'},
        {text: 'test2'},
        {text: 'test3'},
      ],
    }),

    mounted () {
      this.setData()
    },
    methods: {
      setData () {
        this.name = 'betask'
        this.age = '20'
        this.maritalStatus = true
      }
    }
  }
</script>
