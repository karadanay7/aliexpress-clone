<template>
  <div id="AuthPage" class="w-full h-[100vh] bg-white">
    <div
      class="w-full flex items-center justify-center p-5 border-b border-b-gray-300"
    >
      <NuxtLink to="/" class="min-w-[170px]">
        <nuxt-img
          width="170"
          src="/AliExpress-logo.png"
          alt="aliexpresslogo"
          title="aliexpress"
        />
      </NuxtLink>
    </div>

    <div class="max-w-[400px] mx-auto px-2">
      <div class="text-center my-6">Login / Register</div>

      <button
        type="button"
        @click="login('google')"
        class="flex items-center justify-center gap-3 p-1.5 w-full border hover:bg-gray-100 rounded-full text-lg font-semibold"
        id="google"
        aria-label="google"
      >
        <nuxt-img
          class="w-full max-w-[30px]"
          src="/google-logo.png"
          alt="googlelogo"
          title="google-logo"
          sizes="sm:100vw md:50vw lg:400px"
        />
        <div>Google</div>
      </button>

      <button
        type="button"
        @click="login('github')"
        class="mt-4 flex items-center justify-center gap-3 p-1.5 w-full border hover:bg-gray-100 rounded-full text-lg font-semibold"
        id="github"
        aria-label="github"
      >
        <nuxt-img
          class="w-full max-w-[30px]"
          src="/github-logo.png"
          alt="githublogo"
          title="github-logo"
        />
        <div>Github</div>
      </button>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const user = useSupabaseUser();

watchEffect(() => {
  if (user.value) {
    return navigateTo("/");
  }
});

const login = async (prov) => {
  const { data, error } = await client.auth.signInWithOAuth({
    provider: prov,
    redirectTo: window.location.origin,
  });
};
</script>
