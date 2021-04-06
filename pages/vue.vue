<template>
  <NotionRenderer :blockMap="blockMap" fullPage />
</template>

<script>
export default {
  data: () => ({ blockMap: null }),
  async asyncData({ $notion }) {
    // get Notion blocks from the API via a Notion pageId
    const blockMap = await $notion.getPageBlocks("a3f68b3e03c84a44ab166c74bd723633");

    return { blockMap }
  },
};
</script>

<style>
@import "../assets/styles.css"; /* optional Notion-like styles */
</style>
