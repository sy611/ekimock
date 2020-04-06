<template lang="pug">
  v-layout(column justify-center align-center)
    v-flex(xs12 sm8 md6)
      .text-center
        p {{ fill }}
      v-card(width="640")
        v-card-title cardtitle
        v-card-text 
          v-card.my-2.py-0(outlined)
            v-card-title 1st
            v-card-text
              v-select(
                :items="list"
                label="station"
                outlined
                v-model="fill.first.station"
              )
              v-text-field(
                label="minutes"
                outlined
                v-model="fill.first.minutes"
              )
          v-card.my-2.py-0(outlined)
            v-card-title 2nd
            v-card-text
              v-select(
                :items="list"
                label="station"
                outlined
                v-model="fill.second.station"
              )
              v-text-field(
                label="minutes"
                outlined
                v-model="fill.second.minutes"
              )
          
          //- p {{ filtered }}
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
import list from '~/assets/json/list'
import output from '~/assets/json/output'

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data() {
    return {
      output,
      list,
      fill: {
        first: {
          station: '',
          minutes: ''
        },
        second: {
          station: '',
          minutes: ''
        }
      }
    }
  },
  computed: {
    filtered: ''
  }
}
</script>
