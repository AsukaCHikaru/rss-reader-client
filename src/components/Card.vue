<script>
export default {
  props: {
    item: Object,
  }
}
</script>

<template>
  <li>
    <v-card
      max-width="800"
      :color="isHovering ? 'blue-darken-3' : 'blue-darken-4'"
    >
      <a :href="item.link" target="_blank" rel="noopener noreferrer" class="text-decoration-none">
        <v-card-title class="text-blue-lighten-2">
            {{ item.title }}
        </v-card-title>
        <v-card-subtitle class="text-teal-lighten-4">
          <h4>
            {{ item.origin }}
          </h4>
        </v-card-subtitle>
      </a>
    </v-card>
  </li>
</template>

<style scoped>
  li {
    margin: 20px 0;
    width: 100%;
    cursor: pointer;
  }

  a {
    text-decoration: none;
  }
</style>