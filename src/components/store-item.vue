<template>
  <q-card class="my-card">
    <img src="https://cdn.quasar.dev/img/mountains.jpg" />

    <q-card-section>
      <div class="text-h6">{{ product.name }}</div>
      <div class="text-subtitle2">$ {{ product.price }}</div>
    </q-card-section>

    <q-card-section class="q-pt-none ellipsis">
      {{ product.details }}
    </q-card-section>
    <q-card-actions align="right">
      <q-btn
        @click="addToCart()"
        flat
        round
        color="primary"
        icon="add_shopping_cart"
      />
    </q-card-actions>
  </q-card>
</template>
<script>
export default {
  props: ["product"],
  data() {
    return {
      truncate: true,
    };
  },
  methods: {
    addToCart() {
      this.$emit("addToCartEvent", this.product);
      this.$q.notify("Added to cart");
    },
  },
};
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 180px

.zoom
    transition: transform .4s

.zoom:hover
  transform: scale(1.05)
</style>
