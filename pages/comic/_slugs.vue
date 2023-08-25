<template>
    <div class="p-4">
        <h1 class="text-2xl font-bold">{{ comic.title }}</h1>
        <img :src="comic.cover.src" alt="Cover" class="max-w-md mx-auto my-4">
        <nuxt-content :document="comic" class="prose" />
        <div class="mt-4">
            <a :href="comic.links.amazon" class="text-blue-500 hover:underline">Amazon</a>
            <a :href="comic.links.comix" class="text-blue-500 hover:underline ml-2">Comix</a>
        </div>
    </div>
</template>

<script>
export default {
  async asyncData ({ params, $content }) {
    const comic = await $content('comics')
      .where({ slug: params.slug })
      .fetch()
      .then(entries => entries[0])
    console.log({ comic, slug: params.slug })

    return { comic }
  }
}
</script>
