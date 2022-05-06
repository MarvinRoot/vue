<script>
import { ref } from 'vue'
import ReviewList from './ReviewList.vue'
import MyForm from './MyForm.vue';

export default {
    props: {
        premium: Boolean
    },
    data() {
        return {
            product: "Socks",
            brand: "Vue Mastery",
            selectedVariant: 0,
            details: ["50% cotton", "30% wool", "20% polyester"],
            variants: [
                { id: 2234, color: "green", image: "./src/assets/images/socks_green.jpg", quantity: 50 },
                { id: 2235, color: "blue", image: "./src/assets/images/socks_blue.jpg", quantity: 0 },
            ],
            reviews: []
        };
    },
    methods: {
        addToCart() {
            this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
        },
        updateVariant(index) {
            this.selectedVariant = index;
        },
        addReview(review) {
            this.reviews.push(review);
        }
    },
    computed: {
        title() {
            return this.brand + " " + this.product;
        },
        image() {
            return this.variants[this.selectedVariant].image;
        },
        inStock() {
            return this.variants[this.selectedVariant].quantity;
        },
        shipping() {
            if (this.premium) {
                return "Free";
            }
            return 2.99;
        }
    },
    components: { ReviewList, MyForm }

}
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>

        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>

        <p>Shipping: {{ premium? "Free" : 2.99 }}</p>
        <ul>
          <li v-for="detail in details" :key="detail.index">{{ detail }}</li>
        </ul>

        <div 
          v-for="(variant, index) in variants" 
          :key="variant.id" 
          @mouseover="updateVariant(index)" 
          class="color-circle" 
          :style="{ backgroundColor: variant.color }">
        </div>
        
        <button 
          class="button" 
          :class="{ disabledButton: !inStock }" 
          :disabled="!inStock" 
          v-on:click="addToCart">
          Add to Cart
        </button>

      </div>
    </div>
      <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList>
      <MyForm @review-submitted="addReview"></MyForm>
  </div>
</template>

<style scoped>
a {
  color: #062e86;
}
</style>