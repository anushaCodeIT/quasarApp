<template>
  <q-expansion-item
    v-model="expanded"
    class="shadow-1 overflow-hidden"
    style="border-radius: 5px"
    label="Add New"
    header-class="bg-primary text-white"
    expand-icon-class="text-white"
  >
    <q-card>
      <form @submit.prevent="submitForm">
        <q-card-section>
          <div class="q-gutter-y-md column" style="max-width: 600px">
            <q-input
              filled
              v-model="productSubmit.name"
              label="Product Name"
              :rules="[(val) => (val && val.length > 0) || `Required`]"
              ref="name"
            />
            <q-input
              v-model="productSubmit.details"
              label="Product Details"
              filled
              autogrow
            />
            <q-input
              v-model="productSubmit.price"
              label="Product Price"
              filled
              type="number"
              :rules="[
                (val) => (val !== null && val !== '') || 'Required',
                (val) => val >= 0 || 'Invalid',
              ]"
            />
            <q-input
              v-model="productSubmit.count"
              label="Product Count"
              filled
              type="number"
              ref="count"
              :rules="[
                (val) => (val !== null && val !== '') || 'Required',
                (val) => val > 0 || 'Invalid',
              ]"
            />
            <q-btn flat color="primary" label="Save" type="submit" />
          </div>
        </q-card-section>
      </form>
    </q-card>
  </q-expansion-item>
</template>

<script>
import { uid } from "quasar";
export default {
  props: ["product"],
  data() {
    return {
      productSubmit: {
        id: "",
        name: "",
        details: "",
        count: 0,
        price: 0,
        img: "",
      },
      expanded: false,
    };
  },
  watch: {
    product: {
      handler(val) {
        this.productSubmit = val;
        this.expanded = true;
      },
    },
  },
  methods: {
    submitForm() {
      this.$refs.name.validate();
      this.$refs.count.validate();
      if (this.$refs.name.validate() && this.$refs.count.validate()) {
        this.submitProduct();
      }
    },
    submitProduct() {
      let id = uid();
      this.productSubmit.id = id;
      this.$emit("productEvent", this.productSubmit);
      this.expanded = false;
      this.clearFrom();
    },
    clearFrom() {
      this.productSubmit = {
        name: "",
        details: "",
        count: 0,
        price: 0,
        img: "",
      };
    },
  },
};
</script>
<style lang="scss"></style>
