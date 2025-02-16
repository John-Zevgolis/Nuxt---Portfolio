<template>
  <div class="not-prose">
    <section v-if="pending">Loading...</section>
    <section v-else-if="error">Something went wrong... Try again!</section>
    <section v-else>
      <ul class="grid grid-cols-1 gap-4">
        <li
          v-for="project in projects"
          key="project.id"
          class="border border-gray-200 dark:border-gray-800 rounded-sm p-4 hover:bg-gray-200 dark:hover:bg-gray-800"
        >
          <a :href="project.html_url" target="_blank">
            <div class="flex items-center justify-between text-sm">
              <span class="font-semibold">{{ project.name }}</span>
              <span>{{ project.stargazers_count }} *</span>
            </div>
            <p class="text-sm">{{ project.description }}</p>
          </a>
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
const { error, pending, data } = await useFetch(
  "https://api.github.com/users/piotr-jura-udemy/repos"
);

const projects = computed(() => {
  return data.value.sort((a, b) => {
    return b.stargazers_count - a.stargazers_count;
  });
});
</script>
