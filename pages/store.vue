<template>
  <div class="container mx-auto py-8">
    <h1 class="text-3xl font-bold mb-6">Welcome to the Store</h1>

    <header>
      <h1 class="text-2xl font-bold">Store</h1>
      <div class="sorting mt-4">
        <label for="sort" class="block font-medium">Sort by:</label>
        <select id="sort" v-model="sortOption">
          <option value="new">Release Date: New - Old</option>
          <option value="old">Release Date: Old - New</option>
        </select>
      </div>
    </header>

    <aside class="filters flex flex-wrap gap-4 content-around mt-6">
      <h2 class="font-bold w-full">Filters</h2>
      <!-- Genre Filter -->
      <div class="filter-group">
        <h3 class="font-medium">Genre</h3>
        <select v-model="filters.genre">
          <option value="">All</option>
          <option v-for="genre in genres" :key="genre" :value="genre">
            {{ genre }}
          </option>
        </select>
      </div>
      <!-- Price Filter -->
      <div class="filter-group">
        <h3 class="font-medium">Price</h3>
        <select v-model="filters.price">
          <option value="">All</option>
          <option
            v-for="price in priceRanges"
            :key="price.key"
            :value="price.key"
          >
            {{ price.display }}
          </option>
        </select>
      </div>
      <!-- Type Filter -->
      <div class="filter-group">
        <h3 class="font-medium">Type</h3>
        <select v-model="filters.type">
          <option value="">All</option>
          <option v-for="type in types" :key="type.key" :value="type.key">
            {{ type }}
          </option>
        </select>
      </div>
      <!-- Platform Filter -->
      <div class="filter-group">
        <h3 class="font-medium">Platform</h3>
        <div>
          <label v-for="platform in platforms" :key="platform">
            <input
              type="radio"
              name="platform"
              :value="platform"
              v-model="filters.platform"
            />
            {{ platform }}
          </label>
        </div>
      </div>
      <!-- VR, Released, Coming Soon Filters -->
      <div class="filter-group">
        <h3 class="font-medium">Special Filters</h3>
        <label>
          <input type="checkbox" value="vr" v-model="filters.vr" />
          VR
        </label>
        <label>
          <input type="checkbox" value="released" v-model="filters.released" />
          Released
        </label>
        <label>
          <input
            type="checkbox"
            value="comingSoon"
            v-model="filters.comingSoon"
          />
          Coming Soon
        </label>
      </div>
    </aside>

    <main
      class="product-list grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 mt-6"
    >
      <ItemCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
      />
    </main>
  </div>
</template>

<script>
import ItemCard from "@/components/ItemCard.vue";
import productsData from "@/data/data_products.json";
import { computed, ref } from "vue";

export default {
  components: { ItemCard },
  setup() {
    const products = ref(productsData.products);

    const sortOption = ref("new");
    const filters = ref({
      genre: "",
      price: "",
      type: "",
      platform: "",
      vr: false,
      released: false,
      comingSoon: false,
    });

    const genres = ["Action", "Adventure", "Racing", "Sports", "Puzzle"];
    const priceRanges = [
      { key: "0-199", display: "Under $1.99" },
      { key: "200-499", display: "$2.00 - $4.99" },
      { key: "500-999", display: "$5.00 - $9.99" },
    ];
    const types = ["Full Game", "Game Bundle", "Premium Edition"];
    const platforms = ["PS5", "PS4"];

    const filteredProducts = computed(() => {
      let result = products.value;

      // Apply filters
      if (filters.value.genre) {
        result = result.filter((p) => p.genre === filters.value.genre);
      }
      if (filters.value.price) {
        result = result.filter((p) => {
          const price = parseFloat(p.price.discountedPrice.replace("$", ""));
          const [min, max] = filters.value.price.split("-").map(Number);
          return price >= min / 100 && price <= max / 100;
        });
      }
      if (filters.value.type) {
        result = result.filter((p) => p.type === filters.value.type);
      }
      if (filters.value.platform) {
        result = result.filter((p) =>
          p.platforms.includes(filters.value.platform)
        );
      }
      if (filters.value.vr) {
        result = result.filter((p) => p.vr);
      }
      if (filters.value.released) {
        result = result.filter((p) => p.released);
      }
      if (filters.value.comingSoon) {
        result = result.filter((p) => p.comingSoon);
      }

      // Apply sorting
      return result.sort((a, b) => {
        const dateA = new Date(a.releaseDate);
        const dateB = new Date(b.releaseDate);
        return sortOption.value === "new" ? dateB - dateA : dateA - dateB;
      });
    });

    console.log(filteredProducts);

    return {
      filters,
      genres,
      priceRanges,
      types,
      platforms,
      filteredProducts,
      sortOption,
    };
  },
};
</script>
