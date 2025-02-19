<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <h1>hello</h1>
  <table class="border-collapse border border-gray-400">
    <thead>
      <tr>
        <th class="border border-gray-300">State</th>
        <th class="border border-gray-300">City</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="border border-gray-300">Indiana</td>
        <td class="border border-gray-300">Indianapolis</td>
      </tr>
      <tr>
        <td class="border border-gray-300">Ohio</td>
        <td class="border border-gray-300">Columbus</td>
      </tr>
      <tr>
        <td class="border border-gray-300">Michigan</td>
        <td class="border border-gray-300">Detroit</td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
