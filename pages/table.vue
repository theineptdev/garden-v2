<template>
  <div class="container">
    <div class="posts">
        <div class="title">Digital Garden</div>
        <ul>
          <div v-for="(post, k) in posts" :key="k">
            <NuxtLink v-if="post.slug" :to="post.slug" class="post">
                {{ test(post) }}
              <div class="title-tags-date">
                  <div class="post-title">
                    {{ post.title }}
                  </div>
                  <div v-for="(tags, i) in posts" :key="i" class="tags">
                    {{ post.tags[i] }}
                  </div>
                  <div class="date">
                    {{ post.date }}
                  </div>
              </div>
              <div class="preview">
                {{ post.preview }}
              </div>
            </NuxtLink>
          </div>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $notion, params, error }) {
    const pageTable = await $notion.getPageTable("a3f68b3e03c84a44ab166c74bd723633");

    // sort published pages
    const posts = pageTable
      .filter((page) => page.published)
      .sort((a, b) => a.date - b.date);

    // convert array of pages to a map of tags with page arrays
    const postsByTag = pageTable
      .filter((page) => page.published)
      .reduce((map, currentPage) => {
        currentPage.tags.forEach((tag) =>
          map.has(tag)
            ? map.set(tag, [...map.get(tag), currentPage])
            : map.set(tag, [currentPage])
        );
        return map;
      }, new Map());

    return {
      posts,
      postsByTag,
      tags: [...postsByTag.keys()].sort(),
    };
  },
  methods: {
    test(apple) {
        console.log(apple);
        console.log("test");
    }
  }
};
</script>

<style scoped>
.container {
    border: 1px solid red;
    color: white;
    background: #181818;
    height: auto;
    max-height: 100vh;
    width: 100%;
    display: flex;
    flex-direction: column;
    text-align: center;
    overflow-x: hidden;
    font-family: 'Montserrat', sans-serif;
    /* smooth transitions for elements within container */
    transition: 0.25s ease-in-out;
}
.title {
    text-align: center;
    font-size: 2.5rem;
    text-transform: uppercase;
    /* 4.5rem originally */
    padding-top: 4rem;
    padding-bottom: 3rem;
}
.post {
    border: 1px solid blue;
    margin: 0 auto;
    max-width: 35rem;
    /* prevents the width from being 100% on mobile / smaller screens */
    width: 95%;
    /* padding-bottom was 2.5rem */
    padding-bottom: 2rem;
    line-height: 2rem;
    cursor: pointer;
    text-decoration: none;
}
.title-date {
    border: 1px solid yellow;
    display: flex;
    flex-direction: row;
}
.post-title {
    text-decoration: none;
    color: rgba(255, 255, 255, 0.6);
    font-size: 1.75rem;
    text-transform: lowercase;
    display: inline-flex;
    padding-right: 0.25rem;
    overflow-y: hidden;
}
.tags {
    text-decoration: none;
    font-size: 1.75rem;
    text-transform: uppercase;
    color: rgb(126, 126, 126);
    display: inline-flex;
    padding-left: 0.25rem;
}
.date {
    text-decoration: none;
    font-size: 1.75rem;
    text-transform: uppercase;
    color: rgb(56, 56, 56);
    display: inline-flex;
    padding-left: 0.25rem;
}
.preview {
    border: 1px solid red;
    text-decoration: none;
    font-size: 1.25rem;
    color: rgb(90, 90, 90);
    overflow: hidden;
    text-overflow: ellipsis;
    height: 6rem;
}
@media only screen and (min-width: 768px) {
    .post:hover :is(.post-title, .tags, .date, .preview) {
        color: rgba(255, 255, 255, 0.8);
    }
    .post:hover .tags {
        color: rgba(255, 255, 255, 0.7);
    }
    .post:hover .date {
        color: rgba(255, 255, 255, 0.3);
    }
}
</style>
