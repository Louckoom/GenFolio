<script setup>
import Header from "./components/header.vue"
</script>

<template>
  <Header />
  <div id="app">
    <!-- Étape 1 : Choix du style -->
    <div v-if="currentStep === 1">
      <h1>Choisissez votre Thème</h1>
      <StyleInput v-model="selectedTheme" :themes="themes" />
      <button @click="nextStep">Suivant</button>
    </div>

    <!-- Étape 2 : Choix des couleurs -->
    <div v-if="currentStep === 2">
      <h1>Choisissez vos Couleurs</h1>
      <h3>Choisissez votre couleur principale</h3>
      <ColorInput v-model="currentTheme.TextMainColor" :predefinedColors="predefinedColors[0].MainText" />
      <h3>Choisissez votre couleur d'accent</h3>
      <ColorInput v-model="currentTheme.TextSecondColor" :predefinedColors="predefinedColors[1].SecondText" />
      <button @click="prevStep">Précédent</button>
      <button @click="nextStep">Suivant</button>
    </div>

        <div v-if="currentStep === 3">
      <h1>Choisissez votre Font</h1>
      <button @click="prevStep">Précédent</button>
      <button @click="nextStep">Suivant</button>
    </div>

    <!-- Écran de prévisualisation -->
    <Preview :theme="currentTheme" />
  </div>
</template>

<script>
import StyleInput from './components/styleInput.vue';
import Preview from './components/Preview.vue';
import ColorInput from './components/ColorInput.vue';

export default {
  components: {
    StyleInput,
    Preview,
    ColorInput
  },
  data() {
    return {
      themes: [
      { style: 'light-minimalist', primaryColor: '#FFFFFF', accentColor: '#121212', TextMainColor: '#121212', TextSecondColor: '#121212' },  
      { style: 'dark-minimalist', primaryColor: '#121212', accentColor: '#FFFFFF', TextMainColor: '#FFFFFF', TextSecondColor: '#FFFFFF' }
        
      ],
      predefinedColors: [
        {
          MainText: ['#CD2C26', '#B323DB', '#2B9CB5']
        },
        {
          SecondText: ['#F08381', '#E071FF', '#99EBFD']
        }
      ],
      selectedTheme: 'light-minimalist',
      currentStep: 1,
      tempTheme: null // C'est ici que l'on va stocker le thème temporaire
    };
  },
  computed: {
    // Cette propriété calculée renvoie le thème actuel, qu'il soit temporaire ou par défaut
    currentTheme() {
        // Si on est à l'étape 1, on utilise le thème par défaut.
        // Si on est à l'étape 2, on utilise le thème temporaire (qui a été modifié).
        if (this.currentStep === 1) {
            return this.themes.find(theme => theme.style === this.selectedTheme);
        } else {
            return this.tempTheme;
        }
    }
  },
  methods: {
    nextStep() {
      // On clone le thème sélectionné pour pouvoir le modifier
      this.tempTheme = Object.assign({}, this.currentTheme);
      this.currentStep++;
    },
    prevStep() {
      // Quand on revient en arrière, on ne fait rien de spécial,
      // le `currentTheme` va de nouveau pointer vers l'objet original.
      this.currentStep--;
    }
  }
};
</script>

<style lang="scss" scoped>
#app {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 20px;
}
</style>
