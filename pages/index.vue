<template lang="pug">
  v-layout(column justify-center align-center)
    v-flex(xs12 sm8 md6)
      v-card.pb-2.px-1(width="640")
        v-card-title conditions
        v-card-text 
          v-card.my-2.py-0(outlined)
            v-card-title 1st
            v-card-text
              v-select(
                :items="list"
                label="station"
                outlined
                v-model="fill[0].station"
              )
              v-text-field(
                label="minutes"
                outlined
                v-model="fill[0].minutes"
              )
          v-card.my-2.py-0(outlined)
            v-card-title 2nd
            v-card-text
              v-select(
                :items="list"
                label="station"
                outlined
                v-model="fill[1].station"
              )
              v-text-field(
                label="minutes"
                outlined
                v-model="fill[1].minutes"
              )
        
        v-btn(
          block 
          color="primary"
          @click="clickSearch"
        ) search
      
      div.mt-2
        p.display-1 Result
        div
          p 条件を満たす駅
          p {{ calculatored.length }}駅<br />{{ calculatored }}
          
        div.mb-2(v-for="(result, i) in filtered")
          p.font-weight-bold.mb-0 {{ fill[i].station }} まで {{ fill[i].minutes }} 分以内の駅一覧
          p {{ filtered[i].length}}駅<br />{{ filtered[i].map(value => [value.dst, value.time]) }}

        

    
</template>

<script>
import _ from 'lodash'
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
      filtered: [],
      calculatored: [],
      fill: [
        {
          station: '守谷',
          minutes: '60'
        },
        {
          station: '横浜',
          minutes: '40'
        }
      ]
    }
  },
  computed: {},
  methods: {
    clickSearch() {
      console.log('click!!')
      const result = []
      this.fill.forEach((f) => {
        result.push(
          output[f.station].filter((o) => {
            return o.time < f.minutes
          })
        )
      })
      console.log(result)
      this.filtered = [...result]
      // const resultOnlyDst = [...[].concat(...result).map((v) => v.dst)]
      this.calculatored = _.intersection(
        result[0].map((v) => v.dst),
        result[1].map((v) => v.dst)
      )

      // console.log(resultOnlyDst)
      // this.calculatored = getDuplicateValues(
      //   resultOnlyDst.reduce((pre, current) => {
      //     pre.push(...current)
      //     return pre
      //   }, [])
      // ).slice()
    }
  }
}
</script>
