<template>
  <header>
    <nav class="navbar">
      <router-link
        @click="ResetToggleItems"
        class="links branding"
        :to="{ name: 'home' }"
        >SIMBAN</router-link
      >
      <ul class="navbar__main">
        <li class="navbar__main__list" v-for="(item, id) in items" :key="id">
          <router-link
            @click="ResetToggleItems"
            class="links"
            to="#"
            v-if="item.menu.length === 0"
            >{{ item.name }}</router-link
          >
          <div class="main__menu" v-else>
            <router-link class="links" to="#" @click="toggleItems(item.name)"
              >{{ item.name }}<span class="arrow"></span
            ></router-link>
            <ul class="main__menu__submenu" v-if="item.show">
              <router-link
                class="links sub__links"
                to="#"
                v-for="(subitem, id2) in item.menu"
                :key="id2"
                @click="ResetToggleItems"
              >
                {{ subitem.title }}
              </router-link>
            </ul>
          </div>
        </li>
      </ul>

      <!-- Ici on coupe en 2 pour la partie responsive -->
      <div class="toggle__button" @click="toggleMenu">
        <span class="hamburger"></span>
      </div>
      <ul v-if="showMenu" class="navbar__reponsive">
        <li v-for="(item, id) in items" :key="id">
          <router-link
            @click="ResetToggleItems"
            class="links"
            to="#"
            v-if="item.menu.length === 0"
            >{{ item.name }}</router-link
          >
          <div class="responsive__menu" v-else>
            <router-link class="links" to="#" @click="toggleItems(item.name)"
              >{{ item.name }}<span class="arrow"></span
            ></router-link>
            <ul class="responsive__menu__submenu" v-if="item.show">
              <router-link
                class="links sub__links"
                to="#"
                v-for="(subitem, id2) in item.menu"
                :key="id2"
                @click="ResetToggleItems"
              >
                {{ subitem.title }}
              </router-link>
            </ul>
          </div>
        </li>
      </ul>
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
          name: "Région",
          slug: "region",
          menu: [],
          show: false,
        },
        {
          name: "Syndicat",
          menu: [
            { title: "Présentation", slug: "presentation" },
            { title: "Nous contacter", slug: "contact-us" },
            { title: "FAQ", slug: "faq" },
          ],
          show: false,
        },
        {
          name: "Néo-Internes",
          menu: [
            { title: "Informations", slug: "informations" },
            { title: "Formation", slug: "formation" },
            { title: "Choisir la Normandie", slug: "choisir-normandie" },
          ],
          show: false,
        },
        {
          name: "Internes",
          menu: [
            { title: "Stages", slug: "stages" },
            { title: "Vos droits", slug: "vos-droits" },
            { title: "Thèse", slug: "these" },
            { title: "Partenariats", slug: "partenariats" },
            { title: "Evenements", slug: "evenements" },
            { title: "Adresses Locales", slug: "adresses-locales" },
          ],
          show: false,
        },
        {
          name: "Post-Internat",
          menu: [
            { title: "Remplacement", slug: "remplacement" },
            { title: "Aide installation", slug: "aide-installation" },
            { title: "Structures Officiels", slug: "structures-officiels" },
          ],
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
    toggleMenu() {
      console.log(this.showMenu);
      this.showMenu = !this.showMenu;
      this.ResetToggleItems();
    },
  },
  computed: {},
};
</script>

<style lang="scss" scoped>
// Variable sur la hauteur de la navbar (pour prise en compte dans les différenes pages du site)
$height-navbar: 60px;

// navbar definition
.navbar {
  position: fixed;
  width: 100%;
  // height: $height-navbar;
  display: flex;
  align-items: center;
  background-color: $primary-color;
  &__main {
    position: relative;
    display: flex;
    align-items: center;
    &__list {
      // position:relative;
      border: 1px solid black;
      // background: red;

    }
  }
  &__reponsive {
    background-color: $primary-color;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    position: absolute;
    // height: 100vw;
    width: 10%;
    top: 100%;
    right: 0%;
  }
}

.main__menu {
  position: relative;
  &__submenu {
    position: absolute;
    width: 100%;
    background-color: $primary-color;
    top: 100%;
    display: flex;
    flex-direction: column;
  }
  &__items {
    border: 1px solid black;
  }
}

// font n size

// links
.links,
.branding {
  font-weight: 300;
}

.links {
  color: $white-texte;
  padding: 20px;
  text-decoration: none;
  letter-spacing: 1px;
  // border: 1px solid black;
  &:hover {
    color: $hover-color;
    transition: all 0.5s ease-in-out;
  }
}

.sub__links {
  padding: 20px 0 20px 0;
  margin: auto;
  background: red;
  width: 100%;
  font-size: 0.8em;
  z-index: 1000;
  &:hover {
    color: $white-texte;
    background: $hover-color;
    border-radius: 10px;
    transform: scale(1.05);
    transition: all 0.5s ease-in-out;
  }
}
// branding

.branding {
  letter-spacing: 5px;
  font-size: 1.2em;
}

// arrow

// .arrow {
//   position: relative;
//   margin-top: 5px;
//   margin-left: 10px;
//   margin-right: 5px;
//   height: 11px;
//   width: 2px;
//   background-color: transparent;

//   &:after {
//     position: absolute;
//     display: inline-block;
//     content: "";
//     height: 100%;
//     width: 100%;
//     transform: translateX(-3px) rotate(-45deg);
//     background: $white-texte;
//   }
//   &:before {
//     position: absolute;
//     display: inline-block;
//     content: "";
//     height: 100%;
//     width: 100%;
//     transform: translateX(3px) rotate(45deg);
//     background: $white-texte;
//   }
// }

// Hamburger definition

.toggle__button {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  right: 2%;
  width: 45px;
  height: 45px;
  border: 2px solid $white-texte;
  border-radius: 10px;
  cursor: pointer;
  .hamburger {
    width: 65%;
    height: 2px;
    background: $white-texte;
    &:after,
    &:before {
      display: flex;
      content: "";
      width: 100%;
      height: 100%;
      background: $white-texte;
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