<template>
  <h1 class="sr-only">Peek-a-Vue</h1>
  <img src="/images/peek-a-vue-title.png" alt="Peek-a-Vue" class="title" />
  <section :class="$style.description">
    <p>Welcome to Peek-a-Vue, a Halloween themed card matching game!</p>
    <p :class="$style['powered-wrapper']">
      Powered by
      <a :class="$style['powered-link']" href="https://v3.vuejs.org/">
        <img
          :class="$style['powered-logo']"
          src="/images/vue-logo.svg"
          alt="Vue.js logo"
        />
        Vue.js 3
      </a>
      <span>, </span>
      <a
        :class="$style['powered-link']"
        href="https://www.netlify.com/?utm_source=github&utm_medium=peekavue-bh&utm_campaign=devex"
      >
        <img
          :class="$style['powered-logo']"
          src="/images/netliheart.svg"
          alt="Netlify Heart Logo"
        />
        Netlify
      </a>
      <span> & </span>
      <a
        :class="$style['powered-link']"
        href="https://github.com/aevora/Vue/tree/main/peek-a-vue"
      >
        <img
          :class="$style['powered-logo']"
          src="/images/github-logo.svg"
          alt="GitHub Logo"
        />
        GitHub</a
      >
    </p>
  </section>
</template>

<script>
export default {};
</script>

<style module>
.powered-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 15px;
}
.powered-link {
  padding: 0 5px;
  text-decoration: none;
  color: white;
}
.powered-link:first-child,
.powered-link:last-child {
  padding-right: 0;
}
.powered-logo {
  width: 18px;
}

.title {
  padding-bottom: 30px;
}

.description {
  font-family: "Titillium Web", sans-serif;
}

.description p {
  margin: 0;
  font-size: 1.2rem;
}

.description p:last-child {
  margin-bottom: 30px;
}
</style>