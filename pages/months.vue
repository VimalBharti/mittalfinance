<template>
  <div class="w-full h-screen overflow-y-auto">
    <div class="grid grid-cols-3 gap-6 p-6">
        <div class="card bg-gray-500 rounded-2xl shadow-xl border h-full overflow-hidden" v-for="month in months" :key="month">
          <div class="header p-4 text-white">{{ month.name }}</div>
          <div class="body rounded-xl bg-white h-44 p-4 flex flex-col items-center justify-center">
            <h2 class="text-3xl font-bold">22 Clients</h2>
            <NuxtLink to="/" class="text-right w-full flex items-center justify-center gap-1 group text-xs uppercase mt-8">
                <span class="group-hover:font-bold group-hover:border-b border-gray-800">View all</span>
                <Icon name="material-symbols:arrow-right-alt" class="w-5 h-5 group-hover:scale-150 transition duration-700 ease-in-out" />
            </NuxtLink>
          </div>
        </div>
    </div>
  </div>
</template>

<script setup>
  definePageMeta({
    layout: 'dashboard'
  })

  const supabase = useSupabaseClient()

  const months = [
    { number: '01', name: 'January' },
    { number: '02', name: 'February' },
    { number: '03', name: 'March' },
    { number: '04', name: 'April' },
    { number: '05', name: 'May' },
    { number: '06', name: 'June' },
    { number: '07', name: 'July' },
    { number: '08', name: 'August' },
    { number: '09', name: 'September' },
    { number: '10', name: 'October' },
    { number: '11', name: 'November' },
    { number: '12', name: 'December' }
  ]

</script>

<style>

</style>