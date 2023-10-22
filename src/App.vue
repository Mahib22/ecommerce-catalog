<script setup>
import { ref, watchEffect } from 'vue'
import ProductDisplay from './components/ProductDisplay.vue'
import ProductUnavailable from './components/ProductUnavailable.vue'
import IconLoader from './components/icons/IconLoader.vue'

const product = ref([])
const productId = ref(1)
const isLoading = ref(false)
const isUnavailable = ref(false)
const category = { menCategory: "men's clothing", womenCategory: "women's clothing" }

const incrementProductId = () => {
  productId.value > 19 ? (productId.value = 1) : productId.value++
}

watchEffect(async () => {
  isLoading.value = true

  try {
    const response = await fetch(`https://fakestoreapi.com/products/${productId.value}`)
    let data = await response.json()

    if (data.category == category.menCategory || data.category == category.womenCategory) {
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
  <main
    :class="{
      'bg-unavailable': isUnavailable,
      'bg-mens': product.category == category.menCategory,
      'bg-womens': product.category == category.womenCategory
    }"
  >
    <div class="min-h-screen py-24">
      <div class="w-75 bg-light mx-auto rounded-10 shadow">
        <ProductUnavailable v-if="isUnavailable">
          <template #nextButton>
            <button
              class="w-2/5 rounded-4 py-1 border-dark font-semibold text-xl flex mx-auto justify-center items-center gap-2"
              @click="incrementProductId"
            >
              Next product <IconLoader v-if="isLoading" />
            </button>
          </template>
        </ProductUnavailable>

        <ProductDisplay :product="product" :isLoading="isLoading" :category="category" v-else>
          <template #nextButton>
            <button
              class="w-1/2 rounded-4 py-1 border-3 font-semibold text-xl"
              :class="{
                'border-primary text-primary': product.category == category.menCategory,
                'border-purple text-purple': product.category == category.womenCategory
              }"
              @click="incrementProductId"
            >
              Next product
            </button>
          </template>
        </ProductDisplay>
      </div>
    </div>
  </main>
</template>
