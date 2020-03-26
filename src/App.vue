<template>
  <div id="app">
    <router-view name="header" />
    <router-view/>
  </div>
</template>

<script>
import Navbar from './views/layouts/Navbar'
export default {
  name: 'App',
  components: {
    Navbar
  },
  data : function(){
    return {
      status_login: ''
    }
  }
}
</script>