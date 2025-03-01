<template>
  <div class="w-full h-full overflow-y-auto">
    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">All Client</h2>
        <p class="text-gray-400 text-sm">all clients list</p>
      </div>
      <NuxtLink to="/add-client" class="border border-gray-900 text-gray-900 px-4 py-3 rounded-xl w-40 text-sm text-center">Add Client</NuxtLink>
    </header>

    <div class="w-full">
      <UTable :columns="columns" :rows="clients" />
    </div>

  </div>
</template>

<script setup>

  definePageMeta({
      layout: 'dashboard',
      colorMode: 'light',
  });

  const supabase = useSupabaseClient()

  const columns = [{
    key: 'serialnumber',
    label: 'Sr no.'
  }, {
    key: 'fullName',
    label: 'Name'
  }, {
    key: 'phone',
    label: 'Phone'
  }, {
    key: 'loanAmount',
    label: 'Loan Amount'
  }, {
    key: 'loanTenure',
    label: 'Loan Tenure'
  }, {
    key: 'emiStartDate',
    label: 'Loan Start'
  }, {
    key: 'salaryCreditDate',
    label: 'Salary Credit Date'
  }, {
    key: 'role'
  }]

  const months = [
    'January', 'February', 'March', 'April', 'May', 'June',
    'July', 'August', 'September', 'October', 'November', 'December'
  ];
  const years = [
    '2020', '2021', '2022', '2023', '2024', '2025',
    '2026', '2027', '2028', '2029', '2030', '2031',
    '2032', '2033', '2034', '2035', '2036', '2036',
    '2037', '2038', '2039', '2040'
  ];          


  let { data: clients, error } = await supabase
    .from('clients')
    .select('*')
          

</script>

<style>

</style>