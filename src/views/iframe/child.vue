<template>
  <div>
    {{ myname }}
    <a @click="change('adfadf')">aaaa</a>
  </div>
</template>

<script>
  export default {
    name: 'Child',
    props: {
      myname: {
        type: String,
        default: ''
      }
    },
    methods: {
      change (value) {
        console.log(value)
        this.$emit('changeName', value)
      }
    }
  }
</script>

<style scoped>

</style>
