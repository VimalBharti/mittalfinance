<template>
  <div class="w-full h-full overflow-y-auto relative">
    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700" v-if="client">{{ client.fullName }} - Loans</h2>
        <p class="text-gray-400 text-sm">All loans list</p>
      </div>
      <NuxtLink to="/add-client" class="border border-gray-900 text-gray-900 px-4 py-3 rounded-xl w-40 text-sm text-center">Add Loan</NuxtLink>
    </header>

    <template v-if="isLoading">
      <div class="grid grid-cols-6 gap-4 p-4 items-center" v-for="n in 6">
        <USkeleton class="h-16 w-16 rounded-xl" />
        <div class="space-y-2" v-for="n in 5">
          <USkeleton class="h-4 w-full" />
          <USkeleton class="h-4 w-full" />
        </div>
      </div>
    </template>

    <template v-else>
      <div class="w-full grid grid-cols-2 gap-5 p-8">
        <UCard v-for="(loan, index) in loans" :key="loan">
          <template #header>
            <div class="header flex items-center gap-2 text-sm">
              <h3>Loan Number - ({{ index + 1 }})</h3>
              <span></span>
            </div>
          </template>

          <div class="content">
            <ul class="bg-white flex flex-col text-xs">
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border bg-gray-50 border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                <div class="flex items-center justify-between w-full">
                  <span>File Number</span>
                  <span>{{ loan.file_number }}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                <div class="flex items-center justify-between w-full">
                  <span>Loan Amount</span>
                  <span>₹ {{ loan.loan_amount }}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                <div class="flex items-center justify-between w-full">
                  <span>Interest Rate</span>
                  <span>{{ loan.interest_rate }}%</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg dark:bg-neutral-800">
                <div class="flex items-center justify-between w-full">
                  <span>Loan Tenure</span>
                  <span>{{ loan.loan_tenure }} Months</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg dark:bg-neutral-800">
                <div class="flex items-center justify-between w-full">
                  <span>EMI Amount</span>
                  <span>₹ {{ loan.emi_amount }}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg dark:bg-neutral-800">
                <div class="flex items-center justify-between w-full">
                  <span>EMI Start Date</span>
                  <span>{{ loan.emi_start_date }}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg dark:bg-neutral-800">
                <div class="flex items-center justify-between w-full">
                  <span>Salary Credit Date</span>
                  <span>{{ loan.salary_credit_date }}</span>
                </div>
              </li>
              <li class="inline-flex items-center gap-x-2 py-3 px-4 border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg bg-gray-100 font-bold">
                <div class="flex items-center justify-between w-full">
                  <span>Last EMI Date</span>
                  <span>{{ loan.last_emi_date }}</span>
                </div>
              </li>
            </ul>
          </div>

          <template #footer>
            <UAccordion
              :items="actions"
              size="md"
              variant="soft"
              color="gray"
            >
              <!-- previous-emi -->
              <template #previous-emi>
                <div class="">
                  <UTable :columns="columns" :rows="loan.installments" :loading="pending">
                    <template #status-data="{ row }">
                      <UToggle
                        color="green"
                        on-icon="i-heroicons-check-20-solid"
                        off-icon="i-heroicons-x-mark-20-solid"
                        :model-value="row.status"
                      />
                    </template>
                  </UTable>
                </div>
              </template>

              <!-- Add Emi -->
              <template #add-emi>
                <div class="text-gray-900">
                  <div class="grid grid-cols-1 gap-4">
                    
                    <section class="grid grid-cols-2 gap-4">
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          Select Month
                        </span>
                        <UInput v-model="date" type="date" size="lg" />
                      </div>
                      <!-- EMI -->
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          EMI <span class="ml-1 text-xs text-gray-400">(Amount + Interest)</span>
                        </span>
                        <input type="text" class="py-2 px-4 block w-full border-gray-200 rounded-lg sm:text-sm focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none border" placeholder="EMI + Interest" v-model="emi">
                      </div>
                    </section>

                    <section class="grid grid-cols-2 gap-4">
                      <!-- Status for EMI or Not-->
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          Enable/Disable
                        </span>
                        <div class="w-full flex items-center gap-2 border py-2 px-4 rounded-lg">
                          <span class="w-full block text-sm text-gray-700 font-medium">
                            Paying Full Amount
                          </span>
                          <UToggle
                            on-icon="i-heroicons-check-20-solid"
                            off-icon="i-heroicons-x-mark-20-solid"
                            :model-value="false"
                            v-model="status"
                          />
                        </div>
                      </div>
                      <!-- Monthly Status  -->
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          Next Month Salary Date
                        </span>
                        <UInput v-model="loan.salary_credit_date" type="date" size="lg" />
                      </div>
                    </section>

                    <section class="grid grid-cols-2 gap-4" v-if="status === false">
                      <!-- Interest -->
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          Only Interest
                        </span>
                        <input type="text" class="py-2 px-4 block w-full border-gray-200 rounded-lg sm:text-sm focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none border" placeholder="Enter Interest amount" v-model="interest">
                      </div>
                      <!-- Last EMI date -->
                      <div class="w-full">
                        <span class="w-full block text-sm text-gray-700 font-medium">
                          Last EMI Date
                        </span>
                        <input type="date" v-model="newLastEmiDate" class="w-full border rounded-md shadow-sm py-1.5 px-2 text-sm">
                      </div>
                    </section>
                    
                    <UButton 
                      :loading="isSaving" 
                      :color="saveBtnColor" 
                      @click="addEmiToLoan(loan)" 
                      block 
                      :trailing="false"
                      icon="proicons:save"
                      label="Save EMI"
                    />
                  </div>
                </div>
              </template>
            </UAccordion>
          </template>
        </UCard>
      </div>
    </template>

  </div>
</template>

<script setup>

  definePageMeta({
    layout: 'dashboard',
    colorMode: 'light',
  })

  const supabase = useSupabaseClient()
  const route = useRoute()

  const actions = [{
    label: 'Add EMI',
    icon: 'material-symbols-light:contextual-token-add-outline-rounded',
    defaultOpen: false,
    slot: 'add-emi'
  },{
    label: 'Previous EMI',
    icon: 'solar:archive-minimalistic-line-duotone',
    defaultOpen: false,
    slot: 'previous-emi'
  }]

  // Table 
  const columns = [{
    key: 'date',
    label: 'Date'
  }, {
    key: 'emi',
    label: 'EMI'
  }, {
    key: 'interest',
    label: 'Interest(%)'
  }, {
    key: 'status',
    label: 'Status'
  }]

  const client = ref()
  const monthly_status = ref(true)

  const loans = ref([])
  const loansCount = ref(null)
  const newLastEmiDate = ref()

  const isLoading = ref(true)
  const pending = ref(true)

  const isSaving = ref(false)
  const saveBtnColor = ref('cyan')

  const date = ref()
  const emi = ref()
  const interest = ref()
  const status = ref(true)

  const fetchRecords = async () => {
    isLoading.value = true
    
    const { data, error } = await supabase
      .from('clients')
      .select('fullName, file_number')
      .eq('id', route.params.id)
      .single()

    if (error) {
      console.error('Error fetching data:', error)
    } else {
      client.value = data
      isLoading.value = false
    }
    fetchLoanByClient()
  }

  const fetchLoanByClient = async () => {
    let { data, count: total, error } = await supabase
      .from('loans')
      .select("*, installments(date, emi, interest, status)", { count: 'exact' })
      .eq('file_number', client.value.file_number)

    loansCount.value = total
    loans.value = data
    pending.value = false
  }

  const addEmiToLoan = async (event) => {
    isSaving.value = true;
    saveBtnColor.value = 'gray';

    const { data, error } = await supabase
      .from('installments')
      .insert([
        { 
          loan_id : event.id,
          date : date.value,
          emi : emi.value,
          interest : interest.value,
          status : status.value,
        },
      ])
      .select()

      updateSelectedLoan(event);

      isSaving.value = false;
      saveBtnColor.value = 'cyan';

      // Reset values
      date.value = '';
      emi.value = '';
      interest.value = '';
      status.value = false;
  }
  

  // Update Loan Last EMI Date
  const updateSelectedLoan = async (event) => {
    await supabase
      .from('loans')
      .update({ last_emi_date: newLastEmiDate.value, emi_monthly_status: monthly_status.value, salary_credit_date: event.salary_credit_date })
      .eq('id', event.id)

    newLastEmiDate.value = ''
    
    fetchRecords()
  }

  onMounted(fetchRecords)
</script>

<style>

</style>