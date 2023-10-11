<template>
  <nav v-if="notIsLoginPage">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template>

<script>

export default{
  computed:{
    notIsLoginPage(){
      return this.$route.name !== "login";
    }
  }
}

</script>


