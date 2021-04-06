<template>
  <NotionRenderer
    :blockMap="blockMap"
    :pageLinkOptions="pageLinkOptions"
    fullPage
    prism
  />
</template>

<script>
import "prismjs";
import "prismjs/themes/prism.css";

export default {
  data() {
    return {
      pageLinkOptions: { component: "NuxtLink", href: "to" },
    };
  },
  async asyncData({ $notion, params, error }) {
    const pageTable = await $notion.getPageTable("a3f68b3e03c84a44ab166c74bd723633");
    const page = pageTable.find(
      (item) => item.published && item.slug === params.slug
    );
    const blockMap = await $notion.getPageBlocks(page ? page.id : params.slug);
    if (!blockMap || blockMap.error) {
      return error({ statusCode: 404, message: "Post not found" });
    }

    return { blockMap };
  },
};
</script>

<style>
@import "../assets/styles.css";
</style>
