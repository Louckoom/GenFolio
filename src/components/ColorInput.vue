<template>
  <div class="color-picker-container">
    <div class="color-options">
      <!-- S'il y a des couleurs prédéfinies -->
      <div
        v-for="color in predefinedColors"
        :key="color"
        class="color-option"
        :class="{ 'active': color === modelValue }"
        :style="{ backgroundColor: color }"
        @click="$emit('update:modelValue', color)"
      ></div>

      <!-- Le bouton pour ouvrir le color picker -->
      <!-- <label for="custom-color" class="color-option custom-color">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm5 11h-4v4h-2v-4H7v-2h4V7h2v4h4v2z" />
        </svg>
      </label>
      <input type="color" id="custom-color" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" style="display: none;"> -->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: String,
    predefinedColors: Array
  },
  emits: ['update:modelValue']
};
</script>

<style lang="scss" scoped>
.color-picker-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.color-options {
  display: flex;
  gap: 0.5rem;
}

.color-option {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  cursor: pointer;
  border: 6px solid transparent;
  transition: border-color 0.2s ease-in-out;

  &.active {
    border-color: #dddddd;
  }
}

</style>
