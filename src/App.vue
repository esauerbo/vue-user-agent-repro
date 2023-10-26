<script setup>
import { signIn } from 'aws-amplify/auth';
import { setCustomUserAgent } from '@aws-amplify/core/src/Platform/customUserAgent'
import { AuthAction, Category } from '@aws-amplify/core/internals/utils';
import { onMounted, onUnmounted, ref } from 'vue';

const username = ref('');
const password = ref('');

let clearUserAgent;

onMounted(() => {
  clearUserAgent = setCustomUserAgent({
    apis: [
      AuthAction.SignIn,
    ],
    category: Category.Auth,
    additionalDetails: [['Authenticator'], ['ui-vue', '3.2.9']]
  });
});

onUnmounted(() => {
  clearUserAgent();
});

const onSignIn = async () => {
  try {
    const result = await signIn({
      username: username.value,
      password: password.value,
    });
    console.log('Sign up successful:', result);
  } catch (error) {
    console.error('Sign up error:', error);
  }
};

</script>
<template>
  <div>
    <input type="text" v-model="username" placeholder="Username" />
    <input type="password" v-model="password" placeholder="Password" />
    <button @click="onSignIn">Sign In</button>
  </div>
</template>
