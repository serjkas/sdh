<script setup lang="ts">
import { RouterView } from "vue-router"
import AsideComponent from "@/components/AsideComponent.vue"
</script>

<template>
  <el-container>
    <el-aside width="200px">
      <AsideComponent />
    </el-aside>
    <el-main>
      <RouterView />
    </el-main>
  </el-container>
</template>

<style scoped></style>
