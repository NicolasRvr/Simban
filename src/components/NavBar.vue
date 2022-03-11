<template>
  <header>
    <nav class="navbar shadow">
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
                class="navbar__links"
                to="#"
                @click="toggleItems(item.name)"
                >{{ item.name }}<span class="arrow"></span></router-link
              >
              <ul class="submenu shadow" v-if="item.show">
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
          menu: ["Informations", "Formation", "Choisir la Normandie"],
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

<style lang="scss">
// navbar definition
.navbar {
  width:100%;
  position: fixed;
  display: flex;
  align-items: center;
  background-color: $primary-color;
  &__links {
    display: flex;
    color: $white-texte;
    // border: 1px solid black;
    padding: 30px 50px 30px 20px;
    text-decoration: none;
    letter-spacing: 1px;
    font-weight: 300;
  }
  .branding {
    padding-left: 60px;
    letter-spacing: 5px;
    font-size: 1.2em;
    font-weight: 300;
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
      &:hover{
        background: blue;
      }
    }
  }
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
    position:absolute;
    display: inline-block;
    content:"";
    height:100%;
    width:100%;
    transform: translateX(-3px) rotate(-45deg);
    background: $white-texte;
  }
    &:before {
    position:absolute;
    display: inline-block;
    content:"";
    height:100%;
    width:100%;
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