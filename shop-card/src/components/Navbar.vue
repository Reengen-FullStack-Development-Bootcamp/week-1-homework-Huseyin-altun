<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Shoopıng Shoes</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-dropdown variant="info" right>
            <template #button-content>
              <b-icon icon="cart" aria-hidden="true"></b-icon> 
            </template>
            <div v-if="cart.length==0">Sepet Boş</div>
            <div v-for="(item, i) in cart" :key="i">
              <b-dropdown-item-button
                ><button @click="decrement(item)" class="btn btn-danger btn-sm mr-1">-</button>{{ item.title }}
                <button @click="increment(item)" class="btn btn-success btn-sm ml-1">+</button>
                <b-col
                  ><b-badge variant="success">Adet : {{ item.piece }}</b-badge>
                  <b-badge variant="warning"
                    >Numara : {{ item.selectedPrice.size }}</b-badge
                  >
                  <b-badge variant="primary"
                    >Fiyat : {{ item.selectedPrice.price*item.piece }}</b-badge
                  >
                </b-col>
              </b-dropdown-item-button>
              <b-dropdown-divider></b-dropdown-divider>
            </div>
            <b-dropdown-divider></b-dropdown-divider>
            <b-dropdown-item-button  v-if="cart.length>0" variant="danger" @click="deleteAll">
              <b-icon icon="trash2-fill" aria-hidden="true"></b-icon>
              Hepsini Sil
            </b-dropdown-item-button>
             
              
          </b-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    cart: Array,
  },
  methods: {
    deleteAll() {
      this.$emit("deleteAll");
    },
    decrement(item) {
      this.$emit("decrement", item);
    },
    increment(item) {
      this.$emit("increment", item);
    },

    
  },
};
</script>

<style></style>