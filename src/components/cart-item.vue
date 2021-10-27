<template>
  <q-item v-ripple>
    <q-item-section top class="col-2 gt-sm">
      <q-img
        src="https://cdn.quasar.dev/img/mountains.jpg"
        spinner-color="white"
        style="width: 100%"
      />
    </q-item-section>

    <q-item-section top>
      <q-item-label lines="1">
        <span class="text-weight-medium">{{ product.name }}</span>
        <span class="text-grey-8"> ${{ product.price }}</span>
      </q-item-label>

      <q-item-label caption lines="1" style="max-width: 20%">
        <q-input
          v-model="itemQuantity"
          min="1"
          label="Qty"
          type="number"
          :dense="true"
          @change="calItemTotal()"
        />
      </q-item-label>

      <q-item-label
        lines="1"
        class="q-mt-xs text-body2 text-weight-bold text-primary text-uppercase"
      >
      </q-item-label>
    </q-item-section>
    <q-item-section side>
      <div class="text-grey-8 q-gutter-xs vertical-middle">
        <span class="cursor-pointer">$ {{ itemTotalPrice }}</span>
      </div>
    </q-item-section>

    <q-item-section side>
      <div class="text-grey-8 q-gutter-xs vertical-middle">
        <q-btn
          @click="remove(index)"
          class="gt-xs"
          size="12px"
          flat
          dense
          round
          icon="clear"
        />
      </div>
    </q-item-section>
  </q-item>
</template>
<script>
export default {
  props: ["product", "index"],
  data() {
    return {
      truncate: true,
      itemTotalPrice: 0,
      itemQuantity: 1,
    };
  },
  methods: {
    calItemTotal() {
      this.itemTotalPrice = this.product.price * this.itemQuantity;
      let itemTotObj = {
        itemTot: this.itemTotalPrice,
        index: this.index,
      };
      this.$emit("totalAmountEvent", itemTotObj);
    },
    remove(index) {
      this.$emit("removeFromCartEvent", index);
    },
  },
  created() {
    this.calItemTotal();
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
