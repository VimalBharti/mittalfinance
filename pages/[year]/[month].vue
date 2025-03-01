<template>
  <div class="w-full h-full overflow-y-auto">

    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">Client List</h2>
        <p class="text-gray-400 text-sm">List by Salary Credit Date</p>
      </div>
    </header>

    <div class="w-full">
      <!-- <UTable :columns="columns" :rows="clients" /> -->
       <div class="grid grid-cols-2 gap-5 p-6">

        <div class="bg-white border rounded-xl overflow-hidden shadow-sm sm:flex" v-for="client in clients" :key="client">
          <div class="shrink-0 relative rounded-t-xl overflow-hidden pt-[40%] sm:rounded-s-xl w-[40%] md:rounded-se-none">
            <img class="size-full absolute top-0 start-0 object-cover" :src="client.photo" alt="Card Image">
          </div>
          <div class="flex flex-wrap w-full">
            <ul class="flex flex-col w-full">
              <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm text-gray-800 first:mt-0 border-b">
                <div class="flex items-center justify-between w-full">
                  <span>Sr. No.</span>
                  <span>{{client.serialnumber}}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm text-gray-800 first:mt-0 border-b">
                <div class="flex items-center justify-between w-full">
                  <span>Name</span>
                  <span>{{client.fullName}}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm text-gray-800 first:mt-0 border-b">
                <div class="flex items-center justify-between w-full">
                  <span>EMI</span>
                  <span>₹ {{client.emiAmount}}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm text-gray-800 first:mt-0">
                <div class="flex items-center justify-between w-full">
                  <span>Salary Credit Date</span>
                  <span>{{client.salaryCreditDate}}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-semibold bg-gray-50 text-gray-800">
                <div class="flex items-center justify-between w-full">
                  <span>Loan Amount</span>
                  <span>{{ client.loanAmount }}</span>
                </div>
              </li>
            </ul>
          </div>
        </div>

       </div>
    </div>

  </div>
</template>

<script setup>
  definePageMeta({
    layout: 'dashboard',
    colorMode: 'light',
  })

  const supabase = useSupabaseClient()
  const route = useRoute()
  const { year, month } = route.params

  const clients = ref([])

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

  const fetchRecords = async () => {
    const startDate = `${year}-${month}-01`
    const endDate = new Date(year, month, 0).toISOString().split('T')[0]  // Last day of the month
    
    const { data, error } = await supabase
      .from('clients')
      .select('*')
      .gte('salaryCreditDate', startDate)
      .lte('salaryCreditDate', endDate)

    if (error) {
      console.error('Error fetching data:', error)
    } else {
      clients.value = data
    }
  }

  onMounted(fetchRecords)

</script>

<style>

</style>