<template>
  <div class="style-input-container">
    <div class="label-container">
      <label class="input-label">Quel style préférez-vous ?</label>
    </div>
    <div class="theme-options">
      <div
        v-for="theme in themes"
        :key="theme.style"
        :class="['theme-item', { 'active': theme.style === modelValue }]"
        @click="$emit('update:modelValue', theme.style)"
      >
        <span class="theme-name">{{ theme.style }}</span>
        <div class="color-palette">
          <div class="primary-color-box" :style="{ backgroundColor: theme.primaryColor }"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['modelValue', 'themes'],
  emits: ['update:modelValue']
};
</script>

<style lang="scss" scoped>
.style-input-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.label-container {
  font-weight: 500;
  font-size: 1.1rem;
}

.theme-options {
  display: flex;
  gap: 1rem;
}

.theme-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  border: 2px solid #ddd;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  &.active {
    border-color: #000000; // Une couleur pour indiquer la sélection
    box-shadow: 0 0 0 6px rgba(129, 129, 129, 0.2);
  }
}

.theme-name {
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.color-palette {
  display: flex;
  gap: 0.5rem;
}

.primary-color-box,
.accent-color-box {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 1px solid #000000;
}
</style>