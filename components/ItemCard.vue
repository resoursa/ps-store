<template>
  <div class="item-card border rounded shadow-sm p-4 hover:shadow-md">
    <img
      :src="getMasterImage(product.media)"
      :alt="product.name"
      class="w-full h-48 object-cover rounded mb-4"
    />

    <h3 class="text-lg font-semibold truncate" :title="product.name">
      {{ product.name }}
    </h3>

    <p class="text-sm text-gray-500">
      {{ product.localizedStoreDisplayClassification }}
    </p>

    <p class="text-lg font-bold mt-2">
      <span v-if="product.price.isFree">Free</span>
      <span v-else>
        {{ product.price.discountedPrice }}
        <span
          v-if="product.price.discountText"
          class="line-through text-gray-400 ml-2"
        >
          {{ product.price.basePrice }}
        </span>
      </span>
    </p>

    <div v-if="product.platforms.length" class="platforms mt-2">
      <span
        v-for="platform in product.platforms"
        :key="platform"
        class="inline-block px-2 py-1 text-xs text-white rounded bg-blue-500 mr-2"
      >
        {{ platform }}
      </span>
    </div>

    <button
      class="mt-4 bg-blue-600 text-white py-2 px-4 rounded w-full hover:bg-blue-700"
      @click="addToCart"
    >
      Add to Cart
    </button>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },

  // Call placeholder image
  data() {
    return {
      placeholderImage: "https://via.placeholder.com/300x400?text=No+Image",
    };
  },
  methods: {
    // Action that listened by parent component
    addToCart() {
      // Emit an event to notify the parent component
      this.$emit("add-to-cart", this.product);
    },

    // Get the master image of the product from data array
    getMasterImage(media) {
      const masterImage = media.find((item) => item.role === "MASTER");
      return masterImage ? masterImage.url : this.placeholderImage;
    },
  },
};
</script>
