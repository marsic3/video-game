<template>
  <div class="font-sans text-black antialiased">
        <navigation/>
    <nuxt />
  </div>
</template>

<script>
import Navigation from '@/components/Navigation'
import axios from 'axios'

axios.defaults.headers.common['user-key'] = '0588ebd84886dc76e1185eb9658b4302'
axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest'

export default {
  components: {
    Navigation
  }
}
</script>
<style>

</style>
