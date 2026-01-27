<template>
  <div style="height: 100vh">
    <nav>
      <RouterLink to="/create-workflow">Create WorkFlow</RouterLink>
    </nav>
  </div>
  <RouterView />
</template>

<script lang="ts" setup>
import { RouterLink, RouterView } from 'vue-router'
</script>
