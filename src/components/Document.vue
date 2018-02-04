<template>
  <h1>{{ Header }}</h1>
</template>

<script>
import currency from '@/components/Currency'

export default {
  name: 'Document',
  data () {
    return {
      Header: 'Available cryptocurrencies'
    }
  },
  created: {
    LoadData()
  },
  methods: {
    LoadData: function () {

    },
  },
  components: { currency }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
