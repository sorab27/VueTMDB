<template>
  <HeaderComponent />
  <MenuComponent />
  <BodyComponent />
</template>

<script>
import BodyComponent from './BodyComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import MenuComponent from './MenuComponent.vue';

export default {
  components: {
    HeaderComponent,
    MenuComponent,
    BodyComponent
  }
}
</script>
