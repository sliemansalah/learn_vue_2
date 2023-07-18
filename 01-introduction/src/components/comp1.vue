<template>
  <div>
    <br>
      <input @keypress.enter.prevent="saveInput" ref="myInput" v-model="internalMsgComp">
      <br>
      <span>{{ internalMsgComp }}</span>
      <br><br>
  </div>
</template>

<script>
export default {
    props: ['msgComp'],
    data() {
        return {
            internalMsgComp: this.msgComp
        }
    },
    methods: {
        saveInput() {
            this.$emit('saveChildComponent', this.internalMsgComp)
        }
    }
}
</script>

<style>

</style>