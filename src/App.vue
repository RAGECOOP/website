<template>
  <v-app>
    <NavigationComponent />

    <router-view v-slot="{ Component, route }">
      <transition name="fade" mode="out-in" appear>
        <v-main :key="route.name">
          <component :is="Component" />
        </v-main>
      </transition>
    </router-view>
  </v-app>
</template>

<script>
import NavigationComponent from '@/components/Navigation.vue'

export default {
  components: {
    NavigationComponent
  }
}
</script>

<style scoped lang="scss">
@import './styles/_variables.scss';

.fade
{
  &-enter-active,
  &-leave-active
  {
    transition: opacity 0.25s ease;
  }
  
  &-enter-from,
  &-leave-to
  {
    opacity: 0;
  }
}
</style>

<style lang="scss">
:root {
  --rage-color: #ffa500;
}

.text {
  &\:primary {
    color: var(--rage-color)!important;
  }
}

/* NOT ADDED TO VUETIFY YET (3.0.0-beta.4) */
.outline {
  border: thin solid rgba(0, 0, 0, .12)!important;

  &-bottom {
    border-bottom: thin solid rgba(0,0,0,.12);
  }
}
</style>