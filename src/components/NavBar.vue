<template>
  <header>
    <nav class="navbar">
      <router-link
        @click="ResetToggleItems"
        class="navbar__links branding"
        :to="{ name: 'home' }"
        >SIMBAN</router-link
      >
      <div v-if="showMenu" class="navbar__main">
        <ul class="navbar__main__container">
          <li v-for="(item, id) in items" :key="id">
            <router-link
              @click="ResetToggleItems"
              class="navbar__links"
              to="#"
              v-if="item.menu.length === 0"
              >{{ item.name }}</router-link
            >
            <div class="menu__links" v-else>
              <router-link
                class="navbar__links item__arrow"
                to="#"
                @click="toggleItems(item.name)"
                >{{ item.name }}</router-link
              >
              <ul class="submenu" v-if="item.show">
                <router-link
                  class="navbar__links submenu__items"
                  to="#"
                  v-for="(subitem, id2) in item.menu"
                  :key="id2"
                  @click="ResetToggleItems"
                >
                  {{ subitem }}
                </router-link>
              </ul>
            </div>
          </li>
        </ul>
      </div>
      <!-- Ici on coupe en 2 pour la partie responsive -->
      <div class="toggle__button">
        <span class="hamburger"></span>
      </div>
      <div class="responsive_navbar"></div>
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
          name: "Syndicat",
          menu: ["Présentation", "Nous contacter", "FAQ"],
          show: false,
        },
        {
          name: "Néo-Internes",
          menu: ["Informations", "Formation", "Choisir la normandie"],
          show: false,
        },
        {
          name: "Internes",
          menu: [
            "Stages",
            "Vos droits",
            "Thèse",
            "Partenariats",
            "Evenements",
            "Adresses Locales",
          ],
          show: false,
        },
        {
          name: "Post-Internat",
          menu: ["Remplacement", "Aide installation", "Structures Officiels"],
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
    ResetToggleItems() {
      for (const element of this.items) {
        element.show = false;
      }
    },
  },
  computed: {},
};
</script>

<style lang="scss" scoped>
// navbar definition
.navbar {
  position: relative;
  display: flex;
  align-items: center;
  background-color: $button-color;
  &__links {
    display: flex;
    color: $white-texte;
    border: 1px solid black;
    padding: 20px 40px 20px 40px;
    text-decoration: none;
  }
  &__main {
    &__container {
      display: flex;
    }
  }
  &__responsive {
    color: red;
  }
}

// submenu definition
.menu__links {
  position: relative;
  .submenu {
    background-color: $button-color;
    position: absolute;
    display: flex;
    flex-direction: column;
    width: 100%;
    top: 100%;
    &__items {
      margin: auto;
      width: 100%;
    }
  }
}

// item__arrow
.item__arrow {
  position: relative;
  &:after {
    position: absolute;
    top: 45%;
    right: 8%;
    display: inline-block;
    content: "";
    width: 12px;
    height: 12px;
    transform: translate(-50%, -50%) rotate(-45deg);
    border-left: 2px solid white;
    border-bottom: 2px solid white;
  }
}

// Hamburger definition
.toggle__button {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  right: 2%;
  width: 45px;
  height: 45px;
  border: 2px solid white;
  border-radius: 10px;
  cursor: pointer;
  .hamburger {
    width: 65%;
    height: 2px;
    background: white;
    &:after,
    &:before {
      display: flex;
      content: "";
      width: 100%;
      height: 100%;
      background: white;
    }
    &:after {
      transform: translate(0%, -50%) translateY(7.5px);
    }
    &:before {
      transform: translate(0%, -50%) translateY(-7.5px);
    }
  }
}
</style>