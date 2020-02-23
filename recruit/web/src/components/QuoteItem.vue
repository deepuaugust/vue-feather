<template>
  <ul>
    <li class="list-group-item" v-for="author in authors">
      {{author}}
      <ul>
        <li class="list-group-item" v-for="x in groups[author]">{{x.text}}</li>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    groups: { type: Object, required: true },
    authors: { type: Object, required: true },
    quote: { type: Object, required: true }
  }
};
</script>

<style lang="scss" scoped>
</style>
