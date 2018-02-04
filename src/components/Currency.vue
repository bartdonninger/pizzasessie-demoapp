<template>
</template>

<script>
export default {
  name: 'Currency',
  data () {
    return {
      name: '',
      value: null,
      image: null
    }
  },
  created: {
    LoadData()
  },
  methods: {
    LoadData: function () {

    },
    Getimage: function (value) {
      if (value) {
        let image = new Image()
        image.src = 'data:image/png;base64,' + value
        return image
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
