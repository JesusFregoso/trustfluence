<template>
    <UCard class="bg-gray-800 text-white max-w-6xl mx-auto">
      <div class="mb-6 p-8 flex flex-col md:flex-row items-start gap-8">
  <div class="w-full md:w-1/4 mb-4 md:mb-0">
    <img 
      src="https://i.pravatar.cc/300?u=huberman" 
      alt="Andrew Huberman" 
      class="w-full h-auto rounded-full object-cover aspect-square border-4 border-gray-300" 
    />
  </div>
  <div class="w-full md:w-3/4 mt-10">
    <h1 class="text-3xl font-bold">Andrew Huberman</h1>
    <div class="flex flex-wrap gap-2 mt-2">
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Neuroscience</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Sleep</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Performance</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Hormones</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Stress Management</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Exercise Science</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Light Exposure</span>
      <span class="badge outline text-white text-xs px-2 py-1 rounded-full">Circadian Biology</span>
    </div>
    <p class="mt-4 text-sm">
      Stanford Professor of Neurobiology and Ophthalmology, focusing on neural development, brain plasticity, and neural regeneration. Host of the Huberman Lab Podcast, translating neuroscience into practical tools for everyday life. Known for evidence-based approaches to performance, sleep, stress management, and brain optimization.
    </p>
  </div>
</div>
      <!-- Key Metrics Section -->
      <UContainer class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
    <UCard 
      v-for="metric in metrics" 
      :key="metric.title" 
      class="flex flex-col h-full"
    >
      <div class="flex justify-between mb-4">
        <h4 class="text-xl font-semibold text-gray-700 dark:text-gray-200">{{ metric.title }}</h4>
        <UIcon 
          :name="metric.icon" 
          class="w-8 h-8 text-green-400 flex-shrink-0" 
        />
      </div>
      <div class="mb-0">
        <p class="text-2xl">{{ metric.value }}</p>
        <p class="text-sm text-gray-400">{{ metric.description }}</p>
      </div>
    </UCard>
  </UContainer>
  
      <!-- Claims Analysis Section -->
      <div>
        <UContainer>
          <UTabs color="primary" variant="link" :items="tabItems" class="w-full">
          <template #analysis="{ item }">
            <UCard class="flex flex-col h-full mt-10">
          <!-- Search Input -->
          <UFormGroup label="Search claims..." class="mb-4 w-full">
            <UInput
              v-model="searchQuery"
              placeholder="Search claims..."
              icon="i-heroicons-magnifying-glass-20-solid"
              class="w-full"
            />
          </UFormGroup>

    <!-- Filters -->
    <div class="space-y-4 pt-5">
      <!-- Categories Filter -->
      <div>
        <span class="text-sm font-medium mb-2 block">Categories</span>
        <div class="flex flex-wrap gap-2">
          <UBadge
            v-for="category in categories"
            :key="category"
            :color="selectedCategory === category ? 'primary' : 'gray'"
            variant="soft"
            class="cursor-pointer rounded-full"
            @click="selectedCategory = category"
          >
            {{ category }}
          </UBadge>
        </div>
      </div>

      <!-- Verification Status Filter -->
      <div>
        <span class="text-sm font-medium mb-2 block">Verification Status</span>
        <div class="flex flex-wrap gap-2">
          <UBadge
            v-for="status in verificationStatuses"
            :key="status"
            :color="selectedStatus === status ? 'primary' : 'gray'"
            variant="soft"
            class="cursor-pointer"
            @click="selectedStatus = status"
          >
            {{ status }}
          </UBadge>
        </div>
      </div>

      <!-- Sort By Dropdown -->
      <USelect
        v-model="selectedSort"
        :options="sortOptions"
        placeholder="Sort By"
      />
    </div>

    <!-- Active Filters -->
    <div v-if="activeFilters.length" class="mt-4 text-sm text-gray-400">
      <span>Active Filters: </span>
      <span class="font-semibold">{{ activeFilters.join(', ') }}</span>
    </div>
  </UCard>
              <!-- Add your claims analysis content here -->
            </template>
            <template #products="{ item }">
              <!-- Add your recommended products content here -->
            </template>
            <template #monetization="{ item }">
              <!-- Add your monetization content here -->
            </template>

    </UTabs>
  </UContainer>
  
        <UContainer class="space-y-4 mt-10">
          <UCard v-for="claim in claims" :key="claim.id" class="flex items-center justify-between">
            <div>
              <p class="font-semibold">{{ claim.text }}</p>
              <p class="text-sm text-gray-400">{{ claim.status }} | {{ claim.date }}</p>
            </div>
            <div>
              <p :class="claim.trustScore >= 90 ? 'text-green-400' : 'text-yellow-400'">
                {{ claim.trustScore }}% Trust Score
              </p>
              <UButton v-if="claim.source" color="blue" variant="link" size="sm">View Source</UButton>
              <UButton v-if="claim.research" color="blue" variant="link" size="sm">View Research</UButton>
            </div>
          </UCard>
        </UContainer>
      </div>
    </UCard>
  </template>
  
  <script setup>
const metrics = [
  { 
    title: 'Trust Score', 
    value: '89%', 
    description: 'Based on 127 verified claims',
    icon: 'i-heroicons-shield-check'
  },
  { 
    title: 'Yearly Revenue', 
    value: '$5.0M', 
    description: 'Estimated earnings',
    icon: 'i-heroicons-currency-dollar'
  },
  { 
    title: 'Products', 
    value: '1', 
    description: 'Recommended products',
    icon: 'i-heroicons-shopping-bag'
  },
  { 
    title: 'Followers', 
    value: '4.2M+', 
    description: 'Total following',
    icon: 'i-heroicons-users'
  }
]

const activeTab = ref('claim-analysis')

const tabItems = [
  {
    label: 'Claim Analysis',
    slot: 'analysis',
  },
  {
    label: 'Recommended Products',
    slot: 'products',
  },
  {
    label: 'Monetization',
    slot: 'monetization',
  }
]

  const categories = ['All Categories', 'Sleep', 'Performance', 'Hormones', 'Nutrition', 'Exercise', 'Stress', 'Cognition', 'Motivation', 'Recovery', 'Mental Health']
  const statuses = ['All Statuses', 'Verified', 'Questionable', 'Debunked']
  const sortOptions = ['Date']
  
  const selectedCategory = ref('All Categories')
  const selectedStatus = ref('All Statuses')
  const sortBy = ref('Date')
  
  const claims = [
    {
      id: 1,
      text: 'Viewing sunlight within 30-60 minutes of waking enhances cortisol release',
      status: 'Verified',
      date: '14/01/2024',
      trustScore: 92,
      source: true,
      research: true
    },
    {
      id: 2,
      text: 'Non-sleep deep rest (NSDR) protocols can accelerate learning and recovery',
      status: 'Verified',
      date: '09/12/2023',
      trustScore: 88,
      source: false,
      research: false
    }
  ]

  const searchQuery = ref('');
const selectedSort = ref('Date');

const verificationStatuses = ['All Statuses', 'Verified', 'Questionable', 'Debunked'];

const activeFilters = computed(() => {
  const filters = [];
  if (selectedCategory.value !== 'All Categories') filters.push(`Category: ${selectedCategory.value}`);
  if (selectedStatus.value !== 'All Statuses') filters.push(`Status: ${selectedStatus.value}`);
  if (selectedSort.value) filters.push(`Sort By: ${selectedSort.value}`);
  return filters;
});
  </script>
  