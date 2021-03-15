<template>
  <v-row justify="center">
    <v-col cols="12" sm="12">
      <h1 class="text-center">รายละเอียดรถยนต์</h1>
    </v-col>
    <v-col cols="12" sm="4">
      <v-card rounded="lg" min-height="575" color="black">
        <v-toolbar color="light-blue" dark dense flat>
          <v-toolbar-title class="body-3"> {{ name }} </v-toolbar-title>
        </v-toolbar>
        <v-img class="white--text align-end" :src="imgUrl" align="center">
        </v-img>
        <v-card-subtitle>{{ carID }}</v-card-subtitle>
        <v-card-text class="text--primary">
          <div class="dt">
            <v-icon class="ic" x-large> mdi-bitcoin </v-icon> ราคาเช่า
            {{ price }} บาท/วัน
          </div>
          <div class="dt">
            <v-icon class="ic" x-large> mdi-car-seat </v-icon> {{ detail1 }}
          </div>
          <div class="dt">
            <v-icon class="ic" x-large> mdi-treasure-chest </v-icon>
            {{ detail2 }}
          </div>
          <div class="dt">
            <v-icon class="ic" x-large>mdi-car</v-icon> {{ status }}
          </div>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="12" sm="6"
      ><v-card rounded="lg" min-height="500" color="white">
        <v-toolbar color="deep-purple" dark dense flat>
          <v-toolbar-title class="body-3"> ประวัติการเช่า </v-toolbar-title>
        </v-toolbar>
        <v-footer padless>
          <v-col class="text-center" cols="12">
            <v-list-item-title>จำนวนการเช่ารถยนต์ทั้งหมด</v-list-item-title>
          </v-col>
        </v-footer>
        <v-simple-table height="475">
          <template v-slot:default>
            <v-row justify="center">
              <v-simple-table>
                <thead>
                  <tr>
                    <th class="text-left">ชื่อ</th>
                    <th class="text-left">นามสกุล</th>
                    <th class="text-left">เบอร์โทร</th>
                    <th class="text-left">เลขบัตรประชาชน</th>
                    <th class="text-left">รุ่นรถ</th>
                    <!-- <th class="text-left">วันที่เริ่มจอง</th>
            <th class="text-left">วันส่งคืน</th> -->
                    <th class="text-left">รวม</th>
                  </tr>
                  <tr v-for="(i, index) in list" :key="index">
                    <th class="text-left">{{ i.Firstname }}</th>
                    <th class="text-left">{{ i.Lastname }}</th>
                    <th class="text-left">{{ i.Tel }}</th>
                    <th class="text-left">{{ i.numberID }}</th>
                    <th class="text-left">{{ i.carName }}</th>
                    <!-- <th class="text-left">{{ i.DateStart }}</th>
            <th class="text-left">{{ i.DateEnd }}</th> -->
                    <th class="text-left">{{ i.Total }}</th>
                  </tr>
                </thead>
              </v-simple-table></v-row
            >
          </template>
        </v-simple-table>
      </v-card>
    </v-col>

    <v-col cols="12" sm="12"> </v-col>
  </v-row>
</template>

<script>
import { db } from '~/plugins/firebaseConfig.js'
export default {
  data() {
    return {
      list: [],
      carid: this.$route.params.id.carID,
      name: this.$route.params.id.name,
      price: this.$route.params.id.price,
      imgUrl: this.$route.params.id.imgUrl,
      detail1: this.$route.params.id.detail1,
      detail2: this.$route.params.id.detail2,
      status: this.$route.params.id.status,
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
.ic {
  margin-right: 2rem;
}
.dt {
  margin: 1rem;
}
</style>