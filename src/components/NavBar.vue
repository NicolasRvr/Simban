<template>
  <header>
    <nav class="navbar shadow">
      <router-link
        @click="ResetToggleItems"
        class="links branding"
        :to="{ name: 'home' }"
        >SIMBAN</router-link
      >
      <div class="navbar__main">
        <ul class="navbar__main__container">
          <li v-for="(item, id) in items" :key="id">
            <router-link
              @click="ResetToggleItems"
              class="links navbar__main__container__items"
              to="#"
              v-if="item.menu.length === 0"
              >{{ item.name }}</router-link
            >
            <div class="menu__links" v-else>
              <router-link
                class="links navbar__main__container__items"
                to="#"
                @click="toggleItems(item.name)"
                >{{ item.name }}<span class="arrow"></span
              ></router-link>
              <ul class="submenu shadow" v-if="item.show">
                <router-link
                  class="links submenu__items"
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
      </div>
      <!-- Ici on coupe en 2 pour la partie responsive -->
      <div class="toggle__button" @click="toggleMenu">
        <span class="hamburger"></span>
      </div>
      <div v-if="showMenu" class="navbar__responsive shadow">
        <ul class="navbar__responsive__container">
          <li v-for="(item, id) in items" :key="id">
            <router-link
              @click="ResetToggleItems"
              class="links"
              to="#"
              v-if="item.menu.length === 0"
              >{{ item.name }}</router-link
            >
            <div class="menu__links" v-else>
              <router-link class="links" to="#" @click="toggleItems(item.name)"
                >{{ item.name }}<span class="arrow"></span
              ></router-link>
              <ul class="submenu shadow" v-if="item.show">
                <router-link
                  class="links submenu__items"
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
      </div>
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

<style lang="scss">
// Variable sur la hauteur de la navbar (pour prise en compte dans les différenes pages du site)
$height-navbar: 7.5%;

// navbar definition
.navbar {
  // possible de changer pour un parametrage de la hauteur de la navbar en fonction de la hauteur totale de la page
  //  dans ce cas il faudrait changer le padding de chaque links et modifier le relative pour que le submenu tombe bien
  width: 100%;
  height: $height-navbar;
  position: fixed;
  display: flex;
  align-items: center;
  background-color: $primary-color;
  &__main {
    position: relative;
    &__container {
      display: flex;
      &__items {
        padding: 0 50px 0 20px;
        // border: 1px solid black;
      }
    }
  }
  &__responsive {
    position: absolute;
    top: 100%;
    right: 0%;
    width: 15%;
    height: 100vw;
    z-index: 1000;
    background: $primary-color;
    &__container {
      display: flex;
      flex-direction: column;
    }
  }
}

// submenu definition
.menu__links {
  position: relative;
  .submenu {
    background-color: $primary-color;
    position: absolute;
    display: flex;
    flex-direction: column;
    width: 100%;
    top: 100%;
    &__items {
      text-align: left;
      width: 100%;
      padding: 20px 50px 20px 20px;
      font-size: 0.8em;
      &:hover {
        background: $hover-color;
        box-shadow: 0 0 10px $hover-color;
        transform: scale(1.05);
        border-radius: 10px;
        transition: all 0.5s ease-in-out;
        color: $white-texte;
      }
    }
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
  text-decoration: none;
  letter-spacing: 1px;
  &:hover {
    color: $hover-color;
    transition: all 0.5s ease-in-out;
  }
}
// branding

.branding {
  padding-left: 60px;
  padding-right: 20px;
  letter-spacing: 5px;
  font-size: 1.2em;
}

// arrow
.arrow {
  position: relative;
  margin-top: 5px;
  margin-left: 10px;
  margin-right: 5px;
  height: 11px;
  width: 2px;
  background-color: transparent;

  &:after {
    position: absolute;
    display: inline-block;
    content: "";
    height: 100%;
    width: 100%;
    transform: translateX(-3px) rotate(-45deg);
    background: $white-texte;
  }
  &:before {
    position: absolute;
    display: inline-block;
    content: "";
    height: 100%;
    width: 100%;
    transform: translateX(3px) rotate(45deg);
    background: $white-texte;
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