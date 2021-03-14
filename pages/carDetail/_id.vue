<template>
  <v-row justify="center">
    <v-col cols="12" sm="12">
      <h1 class="text-center">รายละเอียดรถยนต์</h1>
    </v-col>
    <v-col cols="12" sm="4">
      <v-card rounded="lg" min-height="575" color="white">
        <v-toolbar color="light-blue" dark dense flat>
          <v-toolbar-title class="body-3"> {{ name }} </v-toolbar-title>
        </v-toolbar>
        <v-img
          class="white--text align-end"
          :src="imgUrl"
          align="center"
        >
        </v-img>
        <v-card-subtitle>{{ carID }}</v-card-subtitle>
        <v-card-text class="text--primary">
          <div class="dt">
            <v-icon class="ic" x-large> mdi-bitcoin </v-icon> ราคาเช่า {{ price }} บาท/วัน
          </div>
          <div class="dt">
            <v-icon class="ic" x-large> mdi-car-seat </v-icon> {{ detail1 }}
          </div>
          <div class="dt">
            <v-icon class="ic" x-large> mdi-treasure-chest </v-icon> {{ detail2 }}
          </div>
          <div class="dt"><v-icon class="ic" x-large>mdi-car</v-icon> {{ status }}</div>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="12" sm="6"
      ><v-card rounded="lg" min-height="500" color="white">
        <v-toolbar color="deep-purple" dark dense flat>
          <v-toolbar-title class="body-3"> ประวัติการเช่า </v-toolbar-title>
        </v-toolbar>
        <v-footer padless>
          <v-col class="text-center" cols="8">
            <v-list-item-title>จำนวนการเช่ารถยนต์ทั้งหมด</v-list-item-title>
          </v-col>
          <v-col class="text-center" cols="4">
            <v-list-item-title class="text-left">5 ครั้ง</v-list-item-title>
          </v-col>
        </v-footer>
        <v-simple-table height="475">
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Name</th>
                <th class="text-left">Income</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in desserts" :key="item.name">
                <td>{{ item.name }}</td>
                <td>{{ item.calories }}</td>
              </tr>
            </tbody>
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