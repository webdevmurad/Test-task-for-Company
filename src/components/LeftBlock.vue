<template>
  <div class="left-block">
  </div>
</template>


<script>

export default {
  name: 'LeftBlock',
  components: {
  }
}
</script>

<style lang="sass">
.left-block 
    width: 50px
    height: 100%
    background-color: #46A0E3

@media (max-width: 500px)
    .left-block 
        display: none

</style>
