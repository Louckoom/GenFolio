<script setup>
import Header from "./components/header.vue"
import PreviewScreen from "./components/Preview.vue"
</script>

<template>
<Header/>
<div class="containerPreview">
<PreviewScreen/>
</div>
</template>

<style lang="scss" scoped>
.containerPreview {
  display: flex;
  justify-content: flex-end;
  margin: 0 20px;
}
</style>
