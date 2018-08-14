<template>
  <div class="menu">
    <h1 class="newYork">{{ active() }}</h1>
    <ul id="menu-list">
      <li v-for="link in links" v-bind:key="link.name"><a href="">{{link.name}}</a></li>
      <li>
          <a href="#" id="menu-icon">menu icon</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  props: ['links', 'selected'],
  data () {
    return {
      some: 'some'
    }
  },
  methods: {
    active: function () {
      return this.links[this.selected].name
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
