<template>
  <header>
    <nav class="container">
      <div class="branding">
        <router-link class="links" :to="{ name: 'home' }">SIMBAN</router-link>
      </div>
      <div v-if="showMenu" class="main__item">
        <ul class="links_container">
          <li v-for="(item, id) in items" :key="id">
            <router-link to="#" v-if="item.menu.length === 0">{{
              item.name
            }}</router-link>
            <div class="item_with_links" v-else>
              <router-link to="#" @click="toggleItems(item.name)">{{
                item.name
              }}</router-link>
              <ul class="submenu" v-if="item.show">
                <router-link
                  class="links submenu_item"
                  to="#"
                  v-for="(subitem, id2) in item.menu"
                  :key="id2"
                >
                  {{ subitem }}
                </router-link>
              </ul>
            </div>
          </li>
        </ul>
      </div>
      <!-- Ici on coupe en 2 pour la partie responsive -->
    </nav>
  </header>
</template>

<script>
export default {
  name: "NavBar",
  components: {},
  data() {
    return {
      showMenu: true,
      items: [
        {
          name: "Accueil",
          menu: [],
          show: false,
        },
        {
          name: "Région",
          menu: [],
          show: false,
        },
        {
          name: "Néo-Internes",
          menu: ["1", "2", "3"],
          show: false,
        },
        {
          name: "Internes",
          menu: ["1", "2", "3"],
          show: false,
        },
        {
          name: "Post-Internat",
          menu: ["1", "2", "3"],
          show: false,
        },
      ],
    };
  },
  methods: {
    toggleItems(input) {
      for (const element of this.items) {
        if (element.name === input) {
          element.show = !element.show;
        } else {
          element.show = false;
        }
      }
    },
  },
  computed: {},
};
</script>

<style lang="scss">
.links {
  color: $white-texte;
  margin: 20px;
  border: 1px solid black;
}

.container {
  display: flex;
  align-items: center;
  border: 1px solid black;
  background-color: $button-color;
  padding: 20px 0px 20px 20px;
}

.name-links,
.links {
  display: flex;
}

.links_container {
  display: flex;
}

p {
  color: red;
  cursor: pointer;
}
</style>