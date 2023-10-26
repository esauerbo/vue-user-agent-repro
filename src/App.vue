<script setup>
  import { signIn } from 'aws-amplify/auth';
  import { setCustomUserAgent } from '@aws-amplify/core/src/Platform/customUserAgent'
  import { AuthAction, Category } from '@aws-amplify/core/internals/utils';
  import { onMounted, onUnmounted, ref } from 'vue';

  const username = ref(''); 
  const password = ref(''); 

  let clearUserAgent; 

  const AUTHENTICATOR_INPUT_BASE = {
  apis: [
    AuthAction.SignUp,
    AuthAction.ConfirmSignUp,
    AuthAction.ResendSignUpCode,
    AuthAction.SignIn,
    AuthAction.ConfirmSignIn,
    AuthAction.FetchUserAttributes,
    AuthAction.SignOut,
    AuthAction.ResetPassword,
    AuthAction.ConfirmResetPassword,
    AuthAction.SignInWithRedirect,
  ],
  category: Category.Auth,
};

  onMounted(() => {
  clearUserAgent = setCustomUserAgent({
    ...AUTHENTICATOR_INPUT_BASE,
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
