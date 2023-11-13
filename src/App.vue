<template>
  <main>
    <h2 class="title">Infinite Scroll</h2>
    <Suspense>
      <infinite-scroll />
      <template #fallback>
        <loader-circular />
      </template>
    </Suspense>
    <p class="made-with-love">Made with &#x2764;&#xfe0f;, by Vitor Ferronato</p>
  </main>
</template>

<script>
import InfiniteScroll from "./components/infinite-scroll.vue";
import LoaderCircular from "./components/Loader-circular.vue";

export default {
  components: { InfiniteScroll, LoaderCircular },
};
</script>

<style scoped>
main {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.title {
  color: #333;
  font-size: 24px;
  margin-bottom: 20px;
}

.made-with-love {
  margin-top: 40px;
  color: #888;
  font-size: 14px;
}
</style>
