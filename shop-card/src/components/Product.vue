<template>
  <div class="mt-3 ml-3">
    <b-container>
      <b-row class="d-flex justify-content-around">
        <b-card
          v-for="(product, i) in products"
          :key="i"
          class="overflow-hidden mt-3"
          :class="product.color === 'dark' ? 'dark-border' : 'blue-border'"
          style=" width:560px"
        >
          <b-row no-gutters>
            <b-col md="6">
              <b-card-img
                :src="product.imageUrl"
                alt="Image"
                class="rounded-3 ml-2"
              ></b-card-img>
              <b-row class="mt-3 ml-2">
                <button
                  class="btn ml-2 mt-1"
                  :class="product.color == 'dark' ? 'dark-button' : 'blue-button' "
                  v-for="(number, i) in product.sizeOfPrice"
                  :key="i"
                  @click="selectNumber(product.id, number.id)"
                >
                  {{ number.size }}
                </button>
              </b-row>
            </b-col>
            <b-col md="6">
              <b-card-body>
                <b-card-text :class="product.color === 'dark' ? 'dark-category' : 'blue-category'">
                  {{ product.category }}
                </b-card-text>
                <b-card-text class="dark-title">
                  {{ product.title }}
                </b-card-text>
                <b-card-text :class="product.color === 'dark' ? 'dark-price' : 'blue-price'">
                  ${{
                    product.sizeOfPrice.find(
                      (x) => x.id == product.selectedPriceId
                    ).price
                  }}
                </b-card-text>
                <b-card-text class="dark-description">
                  {{ product.description }}
                </b-card-text>
                
                <b-form-select
                  v-model="product.piece"
                  :options="options"
                ></b-form-select>
                <b-form-rating
                  v-model="product.star"
                  variant="warning"
                  class="mt-2"
                  readonly
                ></b-form-rating>
                <button
                  @click="addToCart(product)"
                  class="btn btn-md mt-2"
                  :class="product.color === 'dark' ? 'dark-button' : 'blue-button'"
                >
                  SEPETE EKLE 
                </button>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import datashoes from "../static/datashoes.json";
export default {
  name: "Product",
  props: {
    cart: Array,
    products: Array,
  },
  data() {
    return {
      options: datashoes.selectOptions,
      starValue: 3,
    };
  },
  computed: {},
  methods: {
    findProduct(productId) {
      return this.products.find((product) => product.id == productId);
    },
    selectNumber(productId, numberId) {
      let selectedProduct = this.findProduct(productId);
      selectedProduct.selectedPriceId = numberId;
    },
    addToCart(product) {
      this.$emit("addToCart", product);
      this.$bvToast.toast(`Ürün Sepete Eklendi`, {
          title: 'Ürün Eklendi!',
          autoHideDelay: 2000,
          appendToast: true,
          toaster: 'b-toaster-bottom-left'
        })
    },
    
  },
};
</script>

<style>
.dark-button{
  color: #f6f4f5 !important;
  background-color: #252525 !important;
}
.dark-button:hover{
  color: #252525 !important;
  background-color: #f6f4f5 !important;
}
.dark-price{
  font-size:30px;
  color: #252525;
  font-weight: 900;
  text-align: left;
}
.dark-category{
  font-size:15px;
  text-align: left;
  color: #252525;
  font-weight: 700
}
.dark-title{
  font-size: 25px;
  text-align: left;
}
.dark-description{
  font-size:1   3px;
  text-align:left;
}
.blue-button{
  color: #D5F3FE !important;
  background-color: #0F5298 !important;
}
.blue-button:hover{
  color: #0F5298 !important;
  background-color:  #D5F3FE !important;
}
.blue-price{
  font-size:30px;
  font-weight: 900;
  color: #0F5298;
  text-align: left;
}
.blue-category{
  font-size:15px;
  text-align: left;
  color: #0F5298;
  font-weight: 700
}
.dark-border{
  box-shadow: 2px 2px #0c0c0c;
}
.blue-border{
  box-shadow: 2px 2px #2565AE;
}
</style>