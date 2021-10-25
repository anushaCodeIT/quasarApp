<template>
  <q-page class="bg-grey-2 column">
    <!-- <h1>Products</h1> -->
    <!-- <div class="q-pa-md">
      <q-table title="Treats" :data="data" :columns="columns2" row-key="name" />
    </div> -->
    <div class="q-pa-md">
      <productFrom
        :product="editProductData"
        @productEvent="addToList($event)"
      ></productFrom>
    </div>
    <div class="q-pa-md">
      <div>
        <q-chip v-for="product in products" :key="product.name">
          <q-avatar color="red" text-color="white">{{
            product.count
          }}</q-avatar>
          {{ product.name }}
          <q-tooltip>{{ product.name }}</q-tooltip>
        </q-chip>
      </div>
    </div>
    <div class="q-pa-md q-gutter-md">
      <q-list bordered class="rounded-borders" style="max-width: 1000px">
        <q-item-label
          v-if="products.length > 0"
          class="bg-green-1 text-weight-medium"
          header
        >
          {{ products.length }} Product(s) available</q-item-label
        >

        <q-item-label
          v-if="products.length == 0"
          class="bg-green-1 text-weight-medium"
          header
          >No Products</q-item-label
        >

        <div
          class="bg-green-3"
          v-for="(product, index) in products"
          :key="product.name"
        >
          <product
            :product="product"
            :index="index"
            @productDeleteEvent="deleteProduct($event)"
            @productEditEvent="editProduct($event)"
          >
          </product>
        </div>
      </q-list>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default {
  data() {
    return {
      products: [
        // {
        //   id: 1,
        //   name: "Product 01",
        //   details: "This is a amazing product",
        //   count: 10,
        //   price: 500,
        //   img: "https://cdn.quasar.dev/img/avatar.png",
        // },
        // {
        //   id: 2,
        //   name: "Product 02",
        //   details: "This are two amazing product efsdsadas sxcz sadqwe",
        //   count: 15,
        //   price: 400,
        //   img: "https://cdn.quasar.dev/img/avatar.png",
        // },
        // {
        //   id: 3,
        //   name: "Product 04",
        //   details: "This are three amazing product",
        //   count: 134,
        //   price: 50,
        //   img: "https://cdn.quasar.dev/img/avatar.png",
        // },
      ],

      editProductData: { name: "", details: "", count: 0, price: 0, img: "" },
      truncate: true,
    };
  },
  created() {
    console.log(this.data);
  },
  methods: {
    addToList(data) {
      if (this.products) {
        console.log(this.products.filter((item) => item.id == data.id)[0]);
        if (this.products.filter((item) => item.id == data.id)[0]) {
          this.$q.notify("Product Updated");
        } else {
          this.products.push(data);
          this.$q.notify("New Product Added");
        }
      }
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
    },
    editProduct(product) {
      this.editProductData = product;
    },
  },
  components: {
    product: require("components/product.vue").default,
    productFrom: require("components/productForm.vue").default,
  },
};
</script>
