<script setup>
import { RouterLink, RouterView } from 'vue-router'
// import * as token from './utils/token'
</script>

<template>
  <RouterView />
</template>

<style scoped>

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

<script>
import * as token  from './utils/token'
export default {
  mounted(){
    this.checkToken()
  },
  methods: {
    redirectToPage() {
      this.$router.push('/payment');
    },
    async checkToken(){
      if(localStorage.getItem('jwtToken') == "" || localStorage.getItem('jwtToken') == null){
        await token.generateToken("david");
      }

      let tokens = localStorage.getItem('jwtToken');
      
      let status = await token.validateToken(tokens);

      if(status==false){
        localStorage.removeItem("jwtToken");
      }
    },
  },
};
</script>