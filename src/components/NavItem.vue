<template>
  <router-link v-if="!item_size" class="links" to="#">{{
    item.name
  }}</router-link>
  <div class="links" v-else>
    <p @click="toggleItems">{{ item.name }}</p>
    <ul class="submenu" v-if="show">
      <router-link
        class="links submenu_item"
        to="#"
        v-for="(subitem, id) in item.menu"
        :key="id"
      >
        {{ subitem }}
      </router-link>
    </ul>
  </div>
</template>

<script>
export default {
  name: "NavItem",
  props: { item: Object },
  data() {
    return {
      item_size: this.item.menu.length,
      show: false,
    };
  },
  methods: {
    toggleItems() {
      this.show = !this.show;
    },
  },
  computed: {},
};
</script>

<style>
p {
  color: red;
}
</style>