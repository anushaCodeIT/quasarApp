<template>
  <q-page class="bg-grey-2">
    <div class="row">
      <div class="col-8">
        <div class="q-pa-md row items-start q-gutter-md">
          <storeItem
            v-for="product in products"
            :key="product.name"
            :product="product"
            @addToCartEvent="addToCart($event)"
          ></storeItem>
        </div>
      </div>
      <div class="col-4">
        <div class="q-pa-md">
          <q-card flat bordered class="my-card">
            <q-card-section>
              <div class="text-h6">My Cart</div>
            </q-card-section>

            <q-list bordered class="rounded-borders" style="max-width: 600px">
              <cartItem
                v-for="(product, index) in myCart"
                :key="product.name"
                :product="product"
                :index="index"
                @removeFromCartEvent="removeFromCart($event)"
                @totalAmountEvent="updateItemTotalAmount($event)"
              ></cartItem>
            </q-list>
            <q-card-section v-if="!myCart.length">
              <q-item
                ><div class="empty-cart absolute-center">
                  <q-icon
                    name="add_shopping_cart"
                    size="50px"
                    color="primary"
                  />
                  <div class="text-h7 text-primary text-center">Fill me</div>
                </div></q-item
              >
            </q-card-section>
            <q-card-section>
              <div v-if="myCart.length" class="text-subtitle2">
                Total
                <span class="text-subtitle1 float-right"
                  >$ {{ totalAmount }}</span
                >
              </div>

              <q-btn color="primary" class="full-width" label="CHECKOUT" />
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Product 01",
          details: "This is a amazing product",
          count: 10,
          price: 500,
          img: "https://cdn.quasar.dev/img/avatar.png",
        },
        {
          id: 2,
          name: "Product 02",
          details: "This are two amazing product efsdsadas sxcz sadqwe",
          count: 15,
          price: 400,
          img: "https://cdn.quasar.dev/img/avatar.png",
        },
        {
          id: 3,
          name: "Product 04",
          details: "This are three amazing product",
          count: 134,
          price: 50,
          img: "https://cdn.quasar.dev/img/avatar.png",
        },
        {
          id: 3,
          name: "Product 04",
          details: "This are three amazing product",
          count: 134,
          price: 50,
          img: "https://cdn.quasar.dev/img/avatar.png",
        },
      ],
      myCart: [],
      totalAmount: 0,
    };
  },
  methods: {
    addToCart(product) {
      product["itemCount"] = 1;
      product["itemTotAmount"] = product.price;
      this.myCart.push(product);
    },
    removeFromCart(index) {
      this.myCart.splice(index, 1);
      this.$q.notify("Item removed from the cart");
      this.calTotalAmount(index);
    },
    updateItemTotalAmount(item) {
      if (item) {
        this.myCart[item.index].itemTotAmount = item.itemTot;
      }
      this.calTotalAmount();
    },
    calTotalAmount() {
      this.totalAmount = 0;
      for (var i = 0; i < this.myCart.length; i++) {
        this.totalAmount = this.totalAmount + this.myCart[i].itemTotAmount;
        console.log(this.myCart[i].itemTotAmount);
      }
    },
  },
  created() {
    this.calTotalAmount();
  },
  components: {
    storeItem: require("components/store-item.vue").default,
    cartItem: require("components/cart-item.vue").default,
  },
});
</script>

<style lang="scss">
.empty-cart {
  opacity: 0.5;
}
</style>
