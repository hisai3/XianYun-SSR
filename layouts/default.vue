<template>
  <div>
    <Head />
    <nuxt />
    <Footer />
  </div>
</template>
<script>
import Head from "@/components/header.vue";
import Footer from "@/components/footer.vue";
export default {
  components: {
    Head,
    Footer
  }
};
</script>

<style lang="less" >
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

ul,
li,
ol {
  list-style: none;
}

* {
  margin: 0;
  padding: 0;
}

em,
i {
  font-style: normal;
}

a {
  color: inherit;
  text-decoration: none;
}
</style>
