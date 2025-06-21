<script setup>
const slug = useRoute().params.slug;
const { data: post } = await useAsyncData(`blog-${slug}`, () => {
  return queryCollection("blog").path(`/blog/${slug}`).first();
});

const backToTop = () => useRouter().push("/");
</script>

<template>
  <div class="prose prose-invert max-w-prose mx-auto py-7">
    <ContentRenderer :value="post" />
    <button class="mt-4" @click="backToTop">Back to Top</button>
  </div>
</template>
