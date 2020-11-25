<template>
  <div id="app">
    <LeftBlock/>
    <FormBlock/>
  </div>
</template>

<script>

import FormBlock from './components/FormBlock.vue'
import LeftBlock from './components/LeftBlock.vue'

export default {
  name: 'App',
  components: {
    FormBlock,
    LeftBlock
  }
}
</script>

<style lang="sass">
* 
    box-sizing: border-box
    padding: 0
    margin: 0
    font-family: 'Open Sans'

html, body 
    width: 100%
    height: 100%

#app 
    font-family: 'Open Sans'
    -webkit-font-smoothing: antialiased
    -moz-osx-font-smoothing: grayscale
    color: #2c3e50
    display: flex
    flex-direction: column
    overflow: hidden

</style>
