<template>
  <footer class="footer shadow">
    <section class="footer__informations">
      <router-link to="#" class="mentions_legales white" >Mentions Légales</router-link>
      <div class="social-icons white">
        <a v-for="(icon, id) in icons" :key="id" :href="icon.link" target="_blank"
          ><i :class="icon.class"></i
        ></a>
      </div>
    </section>
    <section class="footer__copyright white">Nicolas Rivière</section>
  </footer>
</template>

<script>
export default {
  name: "FootBar",
  components: {},
  data() {
    return {
      icons: [
        { name: "Facebook", link: "https://www.facebook.com/SIMBANIMG", class: "fab fa-facebook" },
        { name: "Instagram", link: "#", class: "fab fa-instagram" },
      ],
    };
  },
  methods: {},
  computed: {},
};
</script>

<style lang="scss">
.footer {
  z-index: 5;
  // position: fixed;
  // bottom: 0;
  width: 100%;
  height: 20%;
  z-index: 0;
  &__informations,
  &__copyright {
    display: flex;
    align-items: center;
  }
  &__informations {
    flex-direction: column;
    justify-content: space-around;
    width: 100%;
    height: 65%;
    background: $secondary-color;
  }
  &__copyright {
    justify-content: center;
    width: 100%;
    height: 35%;
    background: $primary-color;
  }
}

.social-icons {
  i {
    border: 1px solid black;
    padding: 0 20px 0 20px;
    font-size: 200%;
  }
}
</style>