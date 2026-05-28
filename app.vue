<template>
  <div>
    <!-- <NuxtLoadingIndicator /> -->
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup>
const { t, locale, locales } = useI18n();

useHead({
  titleTemplate: `%s | ${t('website_title')}`,
  htmlAttrs: {
    dir: locale.value === 'ar' ? 'rtl' : 'ltr',
    lang: locale.value,
  },
});

useHead({
  link: [
    {
      rel: 'icon',
      type: 'image/ico',
      href: '/img/favicon.ico'
    }
  ],
  // 👇 加到这里，会自动放在 </body> 前
  script: [
    {
      type: 'text/javascript',
      body: true, // 关键：放在 body 末尾
      innerHTML: `
        window.LOKALISE_CONFIG = {
          projectId: "18302045592fa799a35d20.15846093",
          locale: "${locale.value || 'en'}"
        };
        (function () {
          var a = document.createElement("script");
          a.type = "text/javascript";
          a.async = true;
          a.src = "https://app.lokalise.com/live-js/script.min.js?" + new Date().getTime();
          document.body.appendChild(a);
        })();
      `
    }
  ],
  __dangerouslyDisableSanitizers: ['script'] // 允许内联 script
});

const { $i18n } = useNuxtApp();
const languageCookie = useCookie('language');

if (languageCookie.value) {
  $i18n.setLocale(languageCookie.value);
}
</script>

<style lang="scss"></style>
