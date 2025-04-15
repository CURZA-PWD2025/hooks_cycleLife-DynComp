<template>
  <div>
    <h2>Ciclo de vida de un componente y componentes dinámicos con keepAlive</h2>
    <!--  _ = valor del atributo, c= nombre del Atributo  -->
    <button v-for="(_, c) in componentes" @click="currentComponent = c" :class="[{ selected: currentComponent === c }]">
      {{ c }}</button>
    <transition name="fade" mode="out-in">

      <KeepAlive>
        <component :is="componentes[currentComponent]" class="tab"></component>
      </KeepAlive>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import verLista from './components/ComponenteA.vue';
import verCard from './components/ComponenteB.vue';
import ComponenteC from './components/ComponenteC.vue';
import ComponenteD from './components/ComponenteD.vue';
import Hooks from './components/Hooks.vue';

// tipado de atributos para que no tire el warning
type ComponenteKey = keyof typeof componentes
const currentComponent = ref<ComponenteKey>("verLista")

const componentes = {
  verLista, verCard, ComponenteC, ComponenteD, Hooks
}

</script>

<style scoped>
.tab {
  margin: 0 auto;
  height: 350px;
  width: 600px;
  border: 2px solid green;
}

button {
  outline: none;
  border: none;
  border-radius: 0;
}

.selected {
  background-color: green;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(-150px);
}

.fade-enter-active,
.fade-leave-active {
  transition: .5s ease-in-out all;
}
</style>