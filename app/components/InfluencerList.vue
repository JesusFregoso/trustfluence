<script setup lang="ts">
import type { TableColumn } from '@nuxt/ui'

const UAvatar = resolveComponent('UAvatar')

type User = {
  id: number
  rank: number
  name: string
  category: string
  trustScore: number
  trend: string
  followers: string
  username: string
  email: string
  avatar: { src: string }
  company: { name: string }
}

const { data, status } = await useFetch<User[]>('https://jsonplaceholder.typicode.com/users', {
  transform: (data) => {
    return (
      data?.map((user) => ({
        ...user,
        category: 'Health',
        trustScore: 90,
        trend: 'mdi-icon',
        followers: '1m+',
        avatar: { src: `https://i.pravatar.cc/120?img=${user.id}` }
      })) || []
    )
  },
  lazy: true
})


const columns: TableColumn<User>[] = [

  {
    accessorKey: 'id',
    header: 'RANK'
  },
  {
    accessorKey: 'name',
    header: 'INFLUENCER',
    cell: ({ row }) => {
      return h('div', { class: 'flex items-center gap-3' }, [
        h(UAvatar, {
          ...row.original.avatar,
          size: 'lg'
        }),
        h('div', undefined, [
          h('p', { class: 'font-medium text-[var(--ui-text-highlighted)]' }, row.original.name),
          h('p', { class: '' }, `@${row.original.username}`)
        ])
      ])
    }
  },
  {
    accessorKey: 'category',
    header: 'CATEGORY'
  },
  {
    accessorKey: 'trustScore',
    header: 'TRUST SCORE'
  },
  {
    accessorKey: 'trend',
    header: 'TREND'
  },
  {
    accessorKey: 'followers',
    header: 'FOLLOWERS'
  },
  {
    accessorKey: 'verify',
    header: 'VERIFY CLAIMS'
  },
  // {
  //   accessorKey: 'company',
  //   header: 'Company',
  //   cell: ({ row }) => row.original.company.name
  // }
]

// New additions for the header
const activeTab = ref('all')
const searchQuery = ref('')

const statuses = {
  all: 'All',
  active: 'Active',
  inactive: 'Inactive'
}

console.log({statuses})

const tabItems = Object.entries(statuses).map(([key, value]) => ({
  label: value,
  slot: key
}))

console.log({tabItems})

const onFilterTextBoxChanged = (event) => {
  // Implement your filter logic here
  console.log('Search query:', searchQuery.value)
}
</script>

<template>
    <div class="flex-1 divide-y divide-[var(--ui-border-accented)] w-full pt-10">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
  <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-xl font-semibold text-gray-700 dark:text-gray-200">Active Influencers</h3>
      <svg class="w-8 h-8 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
      </svg>
    </div>
    <p class="text-3xl font-bold text-gray-900 dark:text-white">8,742</p>
    <p class="text-sm text-gray-500 dark:text-gray-400">active influencers</p>
    <div class="mt-4 bg-gray-200 dark:bg-gray-700 rounded-full h-2.5">
      <div class="bg-blue-600 h-2.5 rounded-full" style="width: 75%"></div>
    </div>
  </div>

  <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-xl font-semibold text-gray-700 dark:text-gray-200">Claims Verified</h3>
      <svg class="w-8 h-8 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
      </svg>
    </div>
    <p class="text-3xl font-bold text-gray-900 dark:text-white">23,456</p>
    <p class="text-sm text-gray-500 dark:text-gray-400">verified claims</p>
    <div class="mt-4 bg-gray-200 dark:bg-gray-700 rounded-full h-2.5">
      <div class="bg-green-600 h-2.5 rounded-full" style="width: 60%"></div>
    </div>
  </div>

  <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-xl font-semibold text-gray-700 dark:text-gray-200">Average Trust Score</h3>
      <svg class="w-8 h-8 text-indigo-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
      </svg>
    </div>
    <p class="text-3xl font-bold text-gray-900 dark:text-white">85%</p>
    <p class="text-sm text-gray-500 dark:text-gray-400">trust score</p>
    <div class="mt-4 bg-gray-200 dark:bg-gray-700 rounded-full h-2.5">
      <div class="bg-indigo-600 h-2.5 rounded-full" style="width: 85%"></div>
    </div>
  </div>
</div>

    <!-- Header component -->
    <div class="flex items-center gap-2 px-4 py-3.5 overflow-x-auto">

      <div class="flex gap-2">
        <UBadge
          v-for="item in tabItems"
          :key="item.slot"
          :color="activeTab === item.slot ? 'primary' : 'gray'"
          :variant="activeTab === item.slot ? 'solid' : 'outline'"
          @click="activeTab = item.slot"
          class="cursor-pointer rounded-full"
          size="lg"
        >
      {{ item.label }}
    </UBadge>
  </div>
      <UInputGroup :content="{ align: 'end' }" class="ml-auto">
        <UInput
          v-model="searchQuery"
          icon="i-heroicons-magnifying-glass"
          placeholder="Search product..."
          @input="onFilterTextBoxChanged"
        />
      </UInputGroup>
    </div>

    <!-- Existing table component -->
    <UTable :data="data" :columns="columns" :loading="status === 'pending'" class="flex-1" />
  </div>
</template>

<style scoped>
.example-header {
  /* Add any custom styles here */
}
</style>
