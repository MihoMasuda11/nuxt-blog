<script setup>
const route = useRoute();
const router = useRouter();

const slug = route.params.slug;
const { data: post } = await useAsyncData(`blog-${slug}`, () => {
  return queryCollection("blog").path(`/blog/${slug}`).first();
});

const goHome = () => router.push("/");
</script>

<template>
  <main class="prose prose-invert max-w-screen-lg mx-auto py-7 flex gap-8">
    <div class="flex-1">
      <ContentRenderer :value="post" />
      <button class="mt-4" @click="goHome">Back to Home</button>
    </div>

    <aside class="w-64 sticky top-20 self-start">
      <Toc :links="post.body.toc?.links" />
    </aside>
  </main>
</template>
