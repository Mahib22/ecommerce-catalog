<script setup>
defineProps({
  product: Object,
  isLoading: Boolean,
  category: Object
})
</script>

<template>
  <div class="flex flex-col md:flex-row px-6 py-8 items-center">
    <div
      class="md:w-1/3 md:px-6"
      :class="[isLoading ? 'animate-pulse bg-secondary rounded-lg h-60 w-60' : '']"
    >
      <img
        :class="[isLoading ? '' : 'object-cover object-center h-full w-full']"
        :src="isLoading ? '' : product.image"
      />
    </div>

    <div class="md:w-2/3 md:px-8 pt-4 md:pt-0">
      <h1
        :class="[
          isLoading
            ? 'bg-secondary h-5 w-full my-2 animate-pulse rounded'
            : 'font-semibold text-2xl mb-4',
          {
            'text-primary': product.category == category.menCategory,
            'text-purple': product.category == category.womenCategory
          }
        ]"
      >
        {{ isLoading ? '' : product.title }}
      </h1>

      <div class="flex justify-between items-center border-b pb-1">
        <p
          :class="[
            isLoading
              ? 'bg-secondary h-5 w-1/5 my-2 animate-pulse rounded'
              : 'text-dark-soft text-lg font-normal'
          ]"
        >
          {{ isLoading ? '' : product.category }}
        </p>

        <div
          :class="[isLoading ? 'bg-secondary h-5 w-1/3 my-2 animate-pulse rounded' : 'flex gap-2']"
        >
          <p class="text-dark-soft text-lg font-normal">
            {{ isLoading ? '' : `${product.rating?.rate}/5` }}
          </p>
          <div v-if="!isLoading" class="flex items-center gap-0.5">
            <button
              v-for="n in 3"
              :key="n"
              class="rounded-full w-5 h-5"
              :class="{
                'bg-primary': product.category == category.menCategory,
                'bg-purple': product.category == category.womenCategory
              }"
            ></button>
            <button
              v-for="n in 2"
              :key="n"
              class="border-1 rounded-full w-5 h-5"
              :class="{
                'border-primary': product.category == category.menCategory,
                'border-purple': product.category == category.womenCategory
              }"
            ></button>
          </div>
        </div>
      </div>

      <div class="border-b pt-5 pb-10">
        <p
          :class="[
            isLoading
              ? 'bg-secondary h-5 w-1/3 animate-pulse rounded'
              : 'text-xl text-dark font-normal'
          ]"
        >
          {{ isLoading ? '' : product.description }}
        </p>
      </div>

      <h2
        :class="[
          isLoading
            ? 'bg-secondary h-5 w-1/3 my-2 animate-pulse rounded'
            : 'py-2 font-semibold text-2xl',
          {
            'text-primary': product.category == category.menCategory,
            'text-purple': product.category == category.womenCategory
          }
        ]"
      >
        {{ isLoading ? '' : `$${product.price}` }}
      </h2>

      <div class="flex gap-4" v-if="!isLoading">
        <button
          class="w-1/2 rounded-4 py-1 text-light text-xl font-semibold"
          :class="{
            'bg-primary': product.category == category.menCategory,
            'bg-purple': product.category == category.womenCategory
          }"
        >
          Buy now
        </button>
        <slot name="nextButton"></slot>
      </div>
    </div>
  </div>
</template>
