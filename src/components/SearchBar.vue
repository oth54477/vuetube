<template>
  <div>
    <input type="text" v-model="inputData" @keyup.enter="dataToApp">

  </div>
</template>

<script>



export default {
  name: 'SearchBar',
  data: function() {
    return {
      inputData: null
    }
  },
  methods: {
    dataToApp: function () {
      this.$emit('data-to-app', this.inputData)
    },
  },

}
</script>

<style>

</style>