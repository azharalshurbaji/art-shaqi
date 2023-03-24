<template>
  <v-container>
    <v-row>
      <v-col cols="12" lg="6" sm="12">
        <div
          data-aos="fade-right"
          data-aos-duration="2000"  
        >
          <h1 class="text-grey-darken-1 txt_subtitle my-4">
            <v-icon>mdi-cards-diamond</v-icon>
            Earring
            </h1>
        </div>
        </v-col>
    </v-row>
        <v-row
        align="center"
        justify="center"
        >
        <v-col 
          v-for="earring in earrings"
          :key="earring"
          cols="12"
          lg="4"
          sm="5"
          xs="3"
        >
            <v-card 
            flat
            height="auto"
            >
              <v-sheet class="mx-auto" align="center" border>
                <v-img 
                  :src="earring.src"
                  :lazy-src="earring.src"
                  width="300"
                />
                <div
                    class="my-3 text-center"
                    cols="12"
                    lg="4"
                    xs="5"
                    sm="5"
                >
                    <v-sheet class="text-red-darken-1 text-h6">
                        <span class="mr-2 text-h6 text-grey-darken-1">Price:</span>
                        $•{{ earring.price }}
                    </v-sheet>
                        <v-divider class="mx-2 my-2" />
                    <v-sheet class="text-grey-darken-1">
                        {{ earring.title }}
                    </v-sheet>
                    <v-sheet align="center">
                      <v-btn
                        v-if="isLoggedIn"
                        icon="mdi-cart"
                        title="Add to Cart"
                        variant="outlined"
                        class="my-2"
                        color="brown-darken-3"
                        size="50"
                        @click="addToCartEarring(earring)"
                        />
                      <v-btn
                        v-if="isLoggedIn"
                        icon="mdi-shopping"
                        title="Buy Naw"
                        class="my-2 offset-3"
                        color="brown-darken-3"
                        size="50"
                        :to="{ name: 'buy-naw-details', params: { id: earring.id } }"
                        @click="accessoriesDetailsEarring(earring)"
                        />
                    </v-sheet>
                    </div>
                </v-sheet>
            </v-card>
        </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Accessorais from '@/store/Accessorais.js';
import { mapActions, mapState } from 'pinia';
import { useCartStore } from '@/store/cart';
import user from '@/store/user';


export default {

    data:() => ({
        earrings: [
        {
          id: "1e",
          src: "/assets/earring/e-1.png",
          title: "sit amet consectetur adipisicing elit.",
          price: "900"
        },
        {
          id: "2e",
          src: "/assets/earring/e-2.png",
          title: "Hello sit amet consectetur adipisicing elit.",
          price: "800"
        },
        {
          id: "3e",
          src: "/assets/earring/e-3.png",
          title: "sit amet consectetur adipisicing elit.",
          price: "700"
        },
        {
          id: "4e",
          src: "/assets/earring/e-4.png",
          title: "sit amet consectetur adipisicing elit.",
          price: "600"
        },
        {
          id: "5e",
          src: "/assets/earring/e-5.png",
          title: "sit amet consectetur adipisicing elit.",
          price: "500"
        },
        {
          id: "6e",
          src: "/assets/earring/e-6.png",
          title: "sit amet consectetur adipisicing elit.",
          price: "400"
        }
        ],
        
    }),
    created() {
        this.loadEarrings();
    },
  computed: {
    ...mapState(user, ["isLoggedIn" , "user"]),
  },

  methods: {
    loadEarrings() {
      // AccessoraisJSON/earrings.json
      this.axios.get("AccessoraisJSON/earrings.json")
        .then((response) => {
          this.earrings = response.data.earrings;
          // console.log(response);
        })
        .catch((error) => {
          if (error) {
            // alert("Loading failed Earrings API");
            console.log("Loading failed Earrings API");
          }
        });
    },

    ...mapActions(Accessorais , ["accessoriesDetailsEarring"]),
    ...mapActions(useCartStore, ["addToCartEarring"]),
    },

}
</script>

<style>

</style>