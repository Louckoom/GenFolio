<template>
  <div class="font-selector">
    <div class="input-group">
      <label for="title-font">Choisissez votre police de titre</label>
      <select id="title-font" :value="modelValueTitle" @change="$emit('update:modelValueTitle', $event.target.value)">
        <option v-for="font in fonts" :key="font.value" :value="font.value">
          {{ font.name }}
        </option>
      </select>
    </div>
    <div class="input-group">
      <label for="text-font">Choisissez votre police de texte</label>
      <select id="text-font" :value="modelValueText" @change="$emit('update:modelValueText', $event.target.value)">
        <option v-for="font in fonts" :key="font.value" :value="font.value">
          {{ font.name }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modelValueTitle: String,
    modelValueText: String,
    fonts: Array
  },
  emits: ['update:modelValueTitle', 'update:modelValueText']
};
</script>

<style lang="scss" scoped>
.font-selector {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.input-group {
  display: flex;
  flex-direction: column;
}
</style>
