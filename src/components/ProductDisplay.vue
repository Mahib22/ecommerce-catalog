<script setup>
defineProps({
  product: Object,
  isLoading: Boolean
})
</script>

<template>
  <div class="flex flex-col md:flex-row px-6 py-8 items-center">
    <div class="md:w-1/3 md:px-6">
      <img
        :class="[
          isLoading
            ? 'animate-pulse bg-slate-200 rounded-lg h-60'
            : 'object-cover object-center h-full w-full'
        ]"
        :src="isLoading ? '' : product.image"
      />
    </div>

    <div class="md:w-2/3 md:px-8 pt-4 md:pt-0">
      <h1
        :class="[
          isLoading
            ? 'bg-slate-200 h-5 w-full my-2 animate-pulse rounded'
            : 'font-semibold text-2xl mb-4'
        ]"
      >
        {{ isLoading ? '' : product.title }}
      </h1>

      <div class="flex justify-between items-center border-b pb-1">
        <p :class="[isLoading ? 'bg-slate-200 h-5 w-1/5 my-2 animate-pulse rounded' : '']">
          {{ isLoading ? '' : product.category }}
        </p>

        <div
          :class="[isLoading ? 'bg-slate-200 h-5 w-1/3 my-2 animate-pulse rounded' : 'flex gap-2']"
        >
          <p>{{ isLoading ? '' : `${product.rating?.rate}/5` }}</p>
          <div v-if="!isLoading" class="flex gap-1">
            <button
              class="border-2 border-gray-300 rounded-full w-6 h-6 focus:outline-none"
            ></button>
            <button
              class="border-2 border-gray-300 ml-1 bg-gray-700 rounded-full w-6 h-6 focus:outline-none"
            ></button>
            <button
              class="border-2 border-gray-300 ml-1 bg-indigo-500 rounded-full w-6 h-6 focus:outline-none"
            ></button>
          </div>
        </div>
      </div>

      <div class="border-b pt-5 pb-10">
        <p :class="[isLoading ? 'bg-slate-200 h-5 w-1/3 animate-pulse rounded' : '']">
          {{ isLoading ? '' : product.description }}
        </p>
      </div>

      <h2
        :class="[
          isLoading ? 'bg-slate-200 h-5 w-1/3 my-2 animate-pulse rounded' : 'py-2 font-semibold'
        ]"
      >
        {{ isLoading ? '' : `$${product.price}` }}
      </h2>

      <div class="flex gap-4">
        <button class="w-1/2 rounded py-1 bg-gray-600 text-white font-semibold">Buy now</button>
        <slot name="nextButton"></slot>
      </div>
    </div>
  </div>
</template>
