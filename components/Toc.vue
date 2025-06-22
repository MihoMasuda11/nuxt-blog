<script setup lang="ts">
import type { TocLink } from "@nuxt/content";

type TocProps = {
  links?: TocLink[];
};
defineProps<TocProps>();

const router = useRouter();

const scrollToHeader = (id: string) => {
  const tocElement = document.getElementById(id);
  if (tocElement) {
    router.push({ hash: `#${id}` });
    tocElement.scrollIntoView({ behavior: "smooth", block: "center" });
  }
};
</script>

<template>
  <div class="max-h-82 overflow-auto bg-slate-700 px-4 rounded-lg shadow-md">
    <h4>On this page</h4>
    <nav>
      <ul class="pl-0">
        <li
          v-for="{ id, text, children } in links"
          :key="id"
          :id="`toc-${id}`"
          class="mb-2 cursor-pointer list-none text-sm last:mb-0"
          @click="scrollToHeader(id)"
        >
          {{ text }}
          <ul v-if="children" class="pl-2">
            <li
              v-for="child in children"
              :key="child.id"
              class="mb-2 cursor-pointer list-none text-sm last:mb-0"
              @click.stop="scrollToHeader(child.id)"
            >
              {{ child.text }}
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </div>
</template>
