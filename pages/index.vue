<template>
  <div>
    <button @click="updateQuery">Update query</button>
  </div>
</template>

<script setup lang="ts">
const router = useRouter();
const nuxtApp = useNuxtApp();

const query = ref<{ foo: string }>({ foo: "" });
const foo = computed(() => ({ foo: query.value?.foo.toUpperCase() }));

async function updateQuery() {
  query.value = { foo: "bar" };
}

watch(query, () => {
  router.push({ query: query.value });
});

watch(foo, () => {
  // Mimicking external navigateTo
  nuxtApp._scope.stop();
});
</script>
