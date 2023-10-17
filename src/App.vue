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

<style>
button{
    font-weight: bold;
    font-size: 16px;
    width: auto;
    height: auto;
    background: transparent;
    border: solid 4px #f0c808;
    border-radius: 50px;
    color: #f0c808;
    transition: 0.5s;
}

</style>

