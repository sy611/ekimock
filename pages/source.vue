<template lang="pug">
  v-layout
    v-flex.text-center
      //- p {{ output }}
      div.my-2(v-for="(arr, key) in output")
        h1.display-1 {{ key }} からの時間一覧
        v-simple-table.mb-2
          template(v-slot:default)
            thead
              tr
                th.text-center Name
                th.text-center Time(min)
            tbody
              tr(v-for="v in arr" :key="v.src + v.dst")
                td {{ v.dst }}
                td {{ v.time }}
        //- v-card
        //-   v-card-title 出発駅：{{ key }} 
        //-   v-card-text
        //-     span(v-for="v in arr") {{ v.dst }} まで {{ v.time }} 分 <br />
</template>

<script>
import output from '~/assets/json/output'

export default {
  data() {
    return {
      output
    }
  }
}
</script>
