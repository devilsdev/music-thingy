<template>
  <input type="checkbox" v-model="checked" class="gut"/>
</template>

<script>
export default {
  name: 'SoundThing',
  props: ['sound'],
  data () {
    return {
      checked: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gut {
    margin-top: 15px;
    width: 50px;
    height: 50px;
}
</style>
