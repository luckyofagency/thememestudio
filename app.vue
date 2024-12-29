<template>
  <div class="max_container">
    <Header
      :changeLang="changeLang"
      :getCurrentLang="getCurrentLang"
      :lang="lang"
    ></Header>
    <div class="minContainer">
      <NuxtPage :getCurrentLang="getCurrentLang" :lang="lang" />
    </div>
    <Footer
      :changeLang="changeLang"
      :getCurrentLang="getCurrentLang"
      :lang="lang"
    ></Footer>
  </div>
</template>
<style scoped>
.minContainer {
  min-height: 100vh;
}
</style>

<script>
import Header from "~/components/header.vue";
import Footer from "~/components/footer.vue";
export default {
  data() {
    return {
      lang: "en",
    };
  },
  components: {
    Header,
    Footer,
  },
  mounted() {
    if (this.$route.path.includes("/en")) {
      this.lang = "en";
      typeof window !== "undefined" &&
        window.localStorage &&
        localStorage.setItem("currentLang", this.lang);
    } else if (this.$route.path.includes("/ru")) {
      this.lang = "ru";
      typeof window !== "undefined" &&
        window.localStorage &&
        localStorage.setItem("currentLang", this.lang);
    } else {
      typeof window !== "undefined" &&
        window.localStorage &&
        localStorage.setItem("currentLang", "en");
      this.lang = this.getCurrentLang();
    }
  },
  methods: {
    changeLang() {
      this.lang = this.lang === "ru" ? "en" : "ru";
      typeof window !== "undefined" &&
        window.localStorage &&
        localStorage.setItem("currentLang", this.lang);
    },
    getCurrentLang() {
      const storedLang =
        typeof window !== "undefined" &&
        window.localStorage &&
        localStorage.getItem("currentLang");
      return storedLang ? storedLang : "en";
    },
  },
};
</script>