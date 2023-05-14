<template>
  <div :class="{'men-category': isMen, 'women-category': isWomen}">
    <h2>{{ product.title }}</h2>
    <p>{{ product.description }}</p>
    <p>{{ product.price }}</p>
  </div>
</template>

<script>
export default {
  name: 'DisplayCard',
  props: {
    product: {
      type: Object,
      required: true,
    },
    isMen: {
      type: Boolean,
      default: false,
    },
    isWomen: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style>
.men-category {
  background-color: #0000FF;
  color: #FFFFFF;
}

.women-category {
  background-color: #FFC0CB;
  color: #000000;
}
</style>
