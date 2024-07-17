<script lang="ts" setup>
import { Location, Setting } from "@element-plus/icons-vue"

const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
</script>

<template>
  <el-menu router :default-active="$route.path" @open="handleOpen" @close="handleClose">
    <el-menu-item
      :index="
        $router.resolve({
          name: 'home'
        }).path
      "
    >
      <el-icon>
        <location />
      </el-icon>
      <span>Главная</span>
    </el-menu-item>
    <el-menu-item
      :index="
        $router.resolve({
          name: 'test'
        }).path
      "
    >
      <el-icon>
        <setting />
      </el-icon>
      <span>Тест</span>
    </el-menu-item>
  </el-menu>
</template>
