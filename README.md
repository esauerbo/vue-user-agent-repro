#  vue-user-agent
Reproducing an issue where we can't see custom headers in vue when using `setCustomUserAgent`

1. `npm run dev` and go to `http://localhost:3000/`

2. Enter any username/password and click sign in

3. Check network tab and cognito request does not show custom header (missing `Authenticator ui-vue/3.2.9` )