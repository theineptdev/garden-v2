<template>
  <div>
  <NuxtLink class="home-btn" to="/" title="Home"></NuxtLink>
  <NotionRenderer
    :blockMap="blockMap"
    :pageLinkOptions="pageLinkOptions"
    fullPage
    prism
  />
  </div>
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

<style scoped>
* {
  height: 100vh;
  background: #181818;
}

.home-btn {
  background: transparent;
  position: fixed;
  display: flex;
  justify-content: center;
  height: 2rem;
  width: 2rem;
  top: 4.75rem;
  right: 5%;
  content: url('../components/gardenLogoInvFullNoFlipHollow.png');
  filter: grayscale(1) brightness(2);
  opacity: 0.25;
  transition: 0.15s ease-in-out;
}

@media only screen and (min-width: 768px) {
  .home-btn {
    top: 4.5rem;
    right: 6em; 
  }
  .home-btn:hover {
    background: transparent;
    filter: grayscale(0) brightness(1);
    opacity: 1;
  }
}
</style>