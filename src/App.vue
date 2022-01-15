<template>
  <FormRegistration/>
</template>

<script>
import FormRegistration from './components/FormRegistration.vue'

export default {
  name: 'App',
  components: {
    FormRegistration
  }
}
</script>

<style lang="sass">
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  display: flex
  justify-content: center
  color: #2c3e50
  width: 100%
  height: auto
  background-color: #00BFFF

*
  padding: 0
  margin: 0

</style>
