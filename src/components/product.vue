<template>
  <q-item>
    <q-item-section avatar top>
      <q-avatar>
        <q-icon color="grey-9" name="widgets" />
      </q-avatar>
    </q-item-section>

    <q-item-section top>
      <q-item-label class="q-mt-sm text-weight-medium text-primary">{{
        product.name
      }}</q-item-label>
      <q-item-label lines="1">
        <span class="text-weight-medium">$ {{ product.price }}</span>
      </q-item-label>
      <q-item-label caption lines="1">
        {{ product.details }}
      </q-item-label>
      <q-tooltip>{{ product.details }}</q-tooltip>
      <q-item-label
        lines="1"
        class="q-mt-xs text-body2 text-weight-bold text-primary text-uppercase"
      >
        <span class="text-grey-8"> Qty: {{ product.count }}</span>
      </q-item-label>
    </q-item-section>

    <q-item-section top side>
      <div class="text-grey-8 q-gutter-xs">
        <q-btn
          @click="deleteProdunct(index)"
          class="gt-xs"
          size="12px"
          flat
          dense
          round
          icon="delete"
        />
        <q-btn
          @click="editProduct(product)"
          class="gt-xs"
          size="12px"
          flat
          dense
          round
          icon="edit"
        />
        <!-- <q-btn size="12px" flat dense round icon="more_vert" /> -->
      </div>
    </q-item-section> </q-item
  ><q-separator spaced />
</template>
<script>
export default {
  props: ["product", "index"],
  methods: {
    deleteProdunct(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Are you sure to delete this?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.$emit("productDeleteEvent", index);
        });
    },
    editProduct(product) {
      this.$emit("productEditEvent", product);
    },
  },
};
</script>
<style lang="scss"></style>
