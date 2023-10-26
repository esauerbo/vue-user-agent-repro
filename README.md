#  vue-user-agent
Reproducing an issue where we can't see custom headers in vue when using `setCustomUserAgent`

1. Enter any username/password and click sign in

2. Check network tab and cognito request does not show custom header (missing `Authenticator ui-vue/3.2.9` )