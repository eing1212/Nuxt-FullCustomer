<template>
  <div>
    <v-row justify="center">
      <v-simple-table >
       
          <thead>
            <tr>
              <th class="text-left">ชื่อ</th>
              <th class="text-left">นามสกุล</th>
              <th class="text-left">เบอร์โทร</th>
              <th class="text-left">เลขบัตรประชาชน</th>
              <th class="text-left">วันที่เริ่มจอง</th>
              <th class="text-left">วันส่งคืน</th>
              <th class="text-left">รวม</th>
            </tr>
            <tr v-for="(i, index) in list" :key="index">
              <th class="text-left">{{i.Firstname}}</th>
              <th class="text-left">{{i.Lastname}}</th>
              <th class="text-left">{{i.Tel}}</th>
              <th class="text-left">{{i.numberID}}</th>
              <th class="text-left">{{i.DateStart}}</th>
              <th class="text-left">{{i.DateEnd}}</th>
              <th class="text-left">{{i.Total}}</th>
            </tr>
          </thead>
       
      </v-simple-table></v-row
    >
  </div>
</template>

<script>
import { db } from '~/plugins/firebaseConfig.js'
export default {
  data(){
    return {
      list:'',
    }
    
  
  },
  mounted() {
    this.getdata()
  },
methods: {
    // allowedDates: (val) => parseInt(val.split('-')[2], 10) % 2 === 0,
   getdata() {
      db.collection('DBorders')
        .orderBy('numberID', 'asc')
        .onSnapshot((querySnapshot) => {
          const data = []
          querySnapshot.forEach((doc) => {
            data.push(doc.data())
          })
          this.list = data
          console.log(this.list)
        })
    },
  
  },
}
</script>

<style>

</style>