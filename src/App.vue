<template>
  <div id="app">
 <!-- <v-carousel v-if="hacks.length > 0">
  <v-carousel-item :key="i" v-for="i in (hacks.length/10)">
    <v-layout row>
      <v-flex xs4 :key="j" v-for="j in 3">
        <img :src="'https://placehold.it/380x500/?text=' + hacks[(i*3)+j].hid" alt="">
      </v-flex>
    </v-layout>
  </v-carousel-item>
</v-carousel> -->

  <template>
  <v-carousel v-if="hacks.length > 0">
    <v-carousel-item
      v-for="(hack,i) in hacks"
      :key="i"
    >
    <img v-if="hack.images" :src="hack.images[0].url" alt="">
    <img v-if="!hack.images && hack.contentBody[0].text" :src="'https://placehold.it/380x500/?text=' + hack.contentBody[0].text" alt="">
    </v-carousel-item>
  </v-carousel>
</template>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      hacks: []
    }
  },
  mounted: function () {
    axios
      .get('https://mock.crumblyy.com/v2/contents/random/list', {
        headers: {
          'x-api-key':
            '755cba158ad557886b05557a5a5be9bbddf4ad9806f925f653409b3ece18852b0a083f66083426a292f514278d12abe13b6cf645f98709605a90e8310af8873c2a1baa8e931fbbeea6257529bf0f9e3c00f83c841ff66ac9dcba44c323528b474fdba2c37ec271b85e420dc36e8903d3eeae6958d36ce48ec9580a23fbddd41ab390baa24d502e496633ad161fac9ca8fe672198ea2e10cc1b06796c0d595a38b78e665c6a98360177cc9be9886d6300240d6f3e0547ffeb3b456bf152b094bcabc8e3be72205b119caabc588852b852'
        }
      })
      .then(response => {
        console.log(response.data)
        this.hacks = response.data.details
      })
  }
}
</script>
