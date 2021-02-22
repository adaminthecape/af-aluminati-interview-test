<template>
  <div id="app">
    {{/** now tells user what to do **/}}
    Show numbers up to: <input type="number" v-model="limit" />
    <br/>
    Hover over a number to show its divisors:
    <Numbers/>
  </div>
</template>

<script>
  import Numbers from '@/components/Numbers'

  export default {
    name: 'App',
    /** added line breaks **/
    components: {
      Numbers
    },
    /** changed to inline-bracket style **/
    data() {
      return {
        limit: 100
      }
    }
  }
</script>

<style>
</style>
