<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import ProductDisplay from './components/ProductDisplay.vue'
import './assets/index.css'
import { ref } from 'vue'

const premium = ref(true)

</script>

<template>
  <div class="nav-bar"></div>
  <ProductDisplay :premium = "premium" />
 
</template>