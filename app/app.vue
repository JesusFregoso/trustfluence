<template>
  <UApp class="mt-15">
    <div class="ps-px">
      <UNavigationMenu color="primary" :items="items" class="w-full pl-15 pe-15">
        <template #brand>
          <ULink as="button" class="flex items-center gap-2">
            <UIcon 
              name="i-lucide-shield" 
              class="w-6 h-6 text-green-400 flex-shrink-0" 
            />
            <span class="text-lg">TRUSTFLUENCE</span>
          </ULink>
        </template>
      </UNavigationMenu>
    </div>
    <NuxtPage />
  </UApp>
</template>
<script setup lang="ts">
const items = ref([
  [
    {
      label: 'TRUSTFLUENCE',
      slot: 'brand',
      icon: 'i-lucide-shield',
      to: '/',
    }
  ],
  [
    {
      label: 'Guide',
      icon: 'i-lucide-book-open',
      to: '/getting-started'
    },
    {
      label: 'Composables',
      icon: 'i-lucide-database',
      to: '/composables'
    },
    {
      label: 'Components',
      icon: 'i-lucide-box',
      to: '/components',
      active: true
    }
  ]
])
</script>