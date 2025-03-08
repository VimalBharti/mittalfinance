<template>
  <div>
    <span>Select File Number</span>
    <input type="text" placeholder="Select loan" class="border p-2 rounded-xl">
    <br/>
    <span>EMI Month</span>
    <input type="text" placeholder="EMI Month" class="border p-2 rounded-xl">
    <br/>
    <span>EMI Amount</span>
    <input type="text" placeholder="EMI Amount" class="border p-2 rounded-xl">
    <br/>
    <span>EMI Interest</span>
    <input type="text" placeholder="EMI Interest" class="border p-2 rounded-xl">
    <br/>
    <span>Last Month EMI</span>
    <input type="text" placeholder="Last Month EMI" class="border p-2 rounded-xl">
  </div>
</template>

<script setup>
  definePageMeta({
    layout: 'dashboard',
    colorMode: 'light',
  })

  const supabase = useSupabaseClient()
</script>

<style>

</style>