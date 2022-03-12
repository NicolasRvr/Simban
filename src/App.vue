<template>
  <NavBar />
  <router-view />
  <FootBar />
</template>

<script>
// @ is an alias to /src
import NavBar from "@/components/NavBar.vue";
import FootBar from "@/components/FootBar.vue";

export default {
  name: "app",
  components: {
    NavBar,
    FootBar,
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Raleway", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: relative;
  height: 100vh;
  width: 100%;
  font-family: "Raleway", sans-serif;
  font-size: 18px;
  margin: 0;
  padding: 0;
}

.white {
  color: $white-texte;
  text-decoration: none;

  a {
    color: $white-texte;
    text-decoration: none;
  }
}

.shadow {
  box-shadow: 0 0 10px black;
}

// nav {
//   padding: 30px;

//   a {
//     font-weight: bold;
//     color: #2c3e50;

//     &.router-link-exact-active {
//       color: #42b983;
//     }
//   }
// }
</style>
