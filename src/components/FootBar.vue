<template>
  <footer class="footer shadow">
    <section class="footer__informations">
      <a class="mentions_legales white" href="#">Mentions Légales</a>
      <div class="social-icons white">
        <a v-for="(icon, id) in icons" :key="id" :href="icon.link"
          ><i :class="icon.classe"></i
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
        { name: "Facebook", link: "#", classe: "fa-brands fa-facebook" },
        { name: "Instagram", link: "#", classe: "fa-brands fa-instagram" },
      ],
    };
  },
  methods: {},
  computed: {},
};
</script>

<style lang="scss">
.footer {
  position: fixed;
  width: 100%;
  height: 18%;
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
    padding: 0 10px 0 10px;
    font-size: 200%;
  }
}
</style>