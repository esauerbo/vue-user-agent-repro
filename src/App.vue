<script setup>
  import { Authenticator } from '@aws-amplify/ui-vue';
  import { setCustomUserAgent } from '@aws-amplify/core/src/Platform/customUserAgent'
  import '@aws-amplify/ui-vue/styles.css';
  import { onMounted, onUnmounted } from 'vue';
  let clearUserAgent; 

  onMounted(() => {
  clearUserAgent = setCustomUserAgent({
    componentName: 'Authenticator',
    packageName: 'vue',
    version: '3.2.9',
  });
});

onUnmounted(() => {
  clearUserAgent();
});

</script>
<template>
  <authenticator>
    <template v-slot="{ user, signOut }">
      <h1>Hello {{ user.username }}!</h1>
      <button @click="signOut">Sign Out</button>
    </template>
  </authenticator>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
