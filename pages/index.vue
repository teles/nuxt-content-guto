<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">Lista de Comics</h1>
    <div v-for="comic in comics" :key="comic.slug" class="bg-white p-4 rounded-lg shadow mb-4">
      <router-link :to="'/comic/' + comic.slug" class="text-blue-500 hover:underline">
        <h2 class="text-lg font-semibold">{{ comic.title }}</h2>
        <img :src="comic.cover.src" alt="Cover" class="max-w-xs mx-auto my-2">
      </router-link>
      <div class="flex space-x-2">
        <a :href="comic.links.amazon" class="text-blue-500 hover:underline">Amazon</a>
        <a
          v-if="comic.links.panini"
          :href="comic.links.panini"
          class="text-blue-500 hover:underline">
          Panini
        </a>
        <a
          v-if="comic.links.comix"
          :href="comic.links.comix"
          class="text-blue-500 hover:underline">
          Comix
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content }) {
    const comics = await $content('comics').fetch()

    return { comics }
  }
}
</script>
