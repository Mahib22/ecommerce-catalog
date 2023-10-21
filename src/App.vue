<script setup>
import { ref, watchEffect } from 'vue'
import ProductDisplay from './components/ProductDisplay.vue'
import ProductUnavailable from './components/ProductUnavailable.vue'

const product = ref([])
const productId = ref(1)
const isLoading = ref(false)
const isUnavailable = ref(false)

const incrementProductId = () => {
  productId.value > 19 ? (productId.value = 1) : productId.value++
}

watchEffect(async () => {
  isLoading.value = true

  try {
    const response = await fetch(`https://fakestoreapi.com/products/${productId.value}`)
    let data = await response.json()

    if (data.category == "men's clothing" || data.category == "women's clothing") {
      isUnavailable.value = false
      product.value = data
    } else {
      isUnavailable.value = true
    }

    isLoading.value = false
  } catch (error) {
    alert('Terjadi kesalahan saat mengakses API')
  }
})
</script>

<template>
  <main class="bg-gray-200 min-h-screen py-24">
    <div class="w-3/4 bg-white mx-auto rounded-lg shadow-md">
      <ProductUnavailable v-if="isUnavailable">
        <template #nextButton>
          <button
            class="w-2/5 rounded py-1 border-2 border-gray-600 font-semibold"
            @click="incrementProductId"
          >
            Next product
          </button>
        </template>
      </ProductUnavailable>

      <ProductDisplay :product="product" :isLoading="isLoading" v-else>
        <template #nextButton>
          <button
            class="w-1/2 rounded py-1 border-2 border-gray-600 font-semibold"
            @click="incrementProductId"
          >
            Next product
          </button>
        </template>
      </ProductDisplay>
    </div>
  </main>
</template>
