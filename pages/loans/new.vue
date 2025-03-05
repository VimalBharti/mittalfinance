<template>
  <div class="w-full h-full overflow-y-auto">
    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">Add New Loan</h2>
        <p class="text-gray-400 text-sm">add new loan to client</p>
      </div>
      <UButton :loading="isSaving" :color="saveBtnColor" @click="addNewLoan" class="px-4 py-2">Save Details</UButton>
    </header>
    <UProgress animation="carousel" size="sm" color="cyan" v-if="isSaving" />

    <div class="grid grid-cols-12 gap-6 p-6 w-full">

      <!-- Loan Details Section -->
      <div class="w-full col-span-7">
        <section class="bg-white rounded-xl shadow p-4 sm:p-7 dark:bg-neutral-800">
          <div class="mb-5">
            <h2 class="text-xl font-bold text-gray-800">
              Loan Details
            </h2>
            <p class="text-sm text-gray-500">
              Manage loan amount, tenure, interest, docs etc.
            </p>
          </div>

          <!-- Grid -->
          <div class="grid sm:grid-cols-12 gap-2 sm:gap-6 border-t pt-6">
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Select Client
              </label>
            </div>
            <div class="sm:col-span-9">
              <USelectMenu
                searchable
                searchable-placeholder="Search client..."
                class="w-full"
                placeholder="Select client..."
                :options="clients"
                option-attribute="fullName"
                value-attribute="uid"
                v-model="client_id"
              />
            </div>
            <!-- End Col -->

            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Loan Amount
              </label>
            </div>
            <div class="sm:col-span-9">
              <div class="sm:flex rounded-lg shadow overflow-hidden">
                <span class="py-2 px-4 inline-flex items-center min-w-fit w-full bg-gray-50 text-sm text-gray-500 -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:w-auto sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg font-bold">₹</span>
                <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="10000" v-model="loanAmount" @input="calculateEMI">
              </div>
            </div>
            <!-- End Col -->
            
            <!-- Intrest Rate -->
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Interest Rate
              </label>
            </div>
            <div class="sm:col-span-9">
              <div class="sm:flex rounded-lg shadow overflow-hidden">
                <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="3" v-model="interestRate" @input="calculateEMI">
                <span class="py-2 px-4 inline-flex items-center min-w-fit w-full bg-gray-50 text-sm text-gray-500 -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:w-auto sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg font-bold">%</span>
              </div>
            </div>
            <!-- End Col -->

            <!-- Loan Tenure -->
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Loan Tenure
              </label>
            </div>
            <div class="sm:col-span-9">
              <!-- <USelect v-model="loanTenure" :options="tenure" /> -->
              <div class="sm:flex rounded-lg shadow overflow-hidden">
                <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="10" v-model="loanTenure" @input="calculateEMI">
                <span class="py-2 px-4 inline-flex items-center min-w-fit w-full bg-gray-50 text-sm text-gray-500 -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:w-auto sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg">Months</span>
              </div>
            </div>
            <!-- End Col -->

            <!-- Loan Date Start -->
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                EMI Start from
              </label>
            </div>
            <div class="sm:col-span-9 flex space-x-4">
              <!-- <USelect v-model="emiStartMonth" :options="months" placeholder="Select Month" />
              <USelect v-model="emiStartYear" :options="years" placeholder="Select Year" /> -->
              <input type="date" v-model="emiStartDate" class="w-full border rounded-md shadow-sm py-1.5 px-2 text-sm">
            </div>
            <!-- End Col -->

            <!-- EMI Amount -->
            <div class="col-span-12">
              <section class="grid grid-cols-2 gap-4">
                <div>
                  <div class="">
                    <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                      ₹ EMI
                    </label>
                    <span class="text-xs text-gray-400 dark:text-neutral-600 ml-2">(Per month)</span>
                  </div>
                  <div class="">
                    <input type="text" class="py-2 px-3 pe-11 block w-full border border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none bg-gray-100" placeholder="5,000" v-model="emiAmount">
                  </div>
                </div>
                <!-- End Col -->
                <div>
                  <div class="">
                    <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                      % Interest
                    </label>
                    <span class="text-xs text-gray-400 dark:text-neutral-600 ml-2">(Per month)</span>
                  </div>
                  <div class="">
                    <input type="text" class="py-2 px-3 pe-11 block w-full border border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none bg-gray-100" placeholder="Interest amount" v-model="interest_amount_permonth">
                  </div>
                </div>
                <!-- End Col -->
              </section>
            </div>
            <!-- Col ENds -->

            <!-- Salary Credit Date -->
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Salary Credit Date
              </label>
            </div>
            <div class="sm:col-span-9">
              <UPopover :popper="{ placement: 'bottom-start' }">
                <UButton icon="i-heroicons-calendar-days-20-solid" :label="format(date, 'd MMM, yyy')" />

                <template #panel="{ close }">
                  <DatePicker v-model="date" is-required @close="close" />
                </template>
              </UPopover>
            </div>
            <!-- End Col -->

            <!-- Last EMI Date -->
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Last EMI Date
              </label>
            </div>
            <div class="sm:col-span-9 flex space-x-4">
              <!-- <USelect v-model="lastEmiMonth" :options="months" placeholder="Select Month" />
              <USelect v-model="lastEmiYear" :options="years" placeholder="Select Year" /> -->
              <input type="date" v-model="lastEmiDate" class="w-full border rounded-md shadow-sm py-1.5 px-2 text-sm">
            </div>
            <!-- End Col -->

          </div>
          <!-- End Grid -->

        </section>
        <!-- End Section -->
      </div>

      <div class="w-full col-span-5">
        <section class="bg-white rounded-xl shadow p-4 sm:p-7 ">
          <div class="mb-8">
            <h2 class="text-xl font-bold text-gray-800">
              Documents
            </h2>
            <p class="text-sm text-gray-500">
              Adhaar card, PAN card, ATM etc.
            </p>
          </div>

          <div class="w-full">

            <div class="flex items-center gap-5 justify-between">
              <label class="inline-block text-sm text-gray-800 dark:text-neutral-200">
                Documents
              </label>
              <div class="flex gap-x-2">
                <UInput type="file" @change="handleFileChange" icon="i-heroicons-folder" />
                <button @click="uploadImage" :disabled="isUploading" class="w-[50px] h-8 bg-gray-700 text-white rounded">
                  <Icon name="line-md:uploading-loop" v-if="isUploading" />
                  <Icon name="material-symbols:upload-rounded" v-else />
                </button>
              </div>
            </div>
            <!-- End Col -->

          </div>
        </section>
      </div>
      
    </div>

  </div>
</template>

<script setup>
  import { format } from 'date-fns'

  definePageMeta({
      layout: 'dashboard',
      colorMode: 'light',
  });

  const supabase = useSupabaseClient()

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

  const date = ref(new Date())

  const isSaving = ref(false)
  const saveBtnColor = ref('cyan')

  const generateSerial = (prefix = 'MITFIN') => {
    const now = new Date()
    return `${prefix}-${now.getFullYear()}${Math.floor(1000 + Math.random() * 9000)}`
  }

  const client_id = ref();

  const loanAmount = ref();
  const interestRate = ref() //Monthly interest rate (in %);
  const interest_amount_permonth = ref() //Monthly Interest Amount
  const loanTenure = ref();
  const emiAmount = ref(0);
  const emiStartDate = ref();
  const lastEmiDate = ref();
  const serialnumber = ref(generateSerial());

  const imageFile = ref(null)
  const imageUrl = ref('https://hozukjgrfvcuvdtakkte.supabase.co/storage/v1/object/public/website/avatar/avatar.png')
  const isUploading = ref(false)

  // Handle file selection
  const handleFileChange = (event) => {
    // console.log(event[0])
    imageFile.value = event[0];
  }

  // Upload image to Supabase storage
  const uploadImage = async () => {
    if(!imageFile.value) {
      alert('Please select an image file')
      return
    }

    isUploading.value = true
    const fileName = `avatar/${Date.now()}-${imageFile.value.name}`

    // Upload to Supabase Storage (Bucket name: "images")
    const { data, error } = await supabase.storage
      .from('website')
      .upload(fileName, imageFile.value, {
        upsert: false,
        cacheControl: '3600',
      })

    if(error) {
      console.log('Upload failed: ' + error.message)
    } else {
      // Get public URL
      const { data: publicUrlData } = supabase.storage.from('website').getPublicUrl(fileName)
      imageUrl.value = publicUrlData.publicUrl
    }
    isUploading.value = false
  }


  let { data: clients, error } = await supabase
    .from('clients')
    .select('fullName, uid')
  

  const addNewLoan = async () => {
    isSaving.value = true;
    saveBtnColor.value = 'gray';

    const { data, error } = await supabase
      .from('loans')
      .insert([
        { 
          client_id: client_id.value,
          serial_number: serialnumber.value,
          loan_amount : loanAmount.value,
          interest_rate : interestRate.value,
          interest_amount_permonth : interest_amount_permonth.value,
          loan_tenure : loanTenure.value,
          emi_amount : emiAmount.value,
          emi_start_date : emiStartDate.value,
          last_emi_date : lastEmiDate.value,
          salary_credit_date : date.value,
          documents : imageUrl.value
        },
      ])
      .select()

      isSaving.value = false;
      saveBtnColor.value = 'cyan';

      // Reset values
      client_id.value = '';
      loanAmount.value = '';
      interestRate.value = ''
      interest_amount_permonth.value = ''
      loanTenure.value = '';
      emiAmount.value = 0;
      emiStartDate.value = '';
      lastEmiDate.value = '';
      imageUrl.value = '';
      serialnumber.value = ref(generateSerial());

  }

  // Function to calculate EMI
  const calculateEMI = () => {
    const P = loanAmount.value
    const r = interestRate.value / 100 * P
    const n = loanTenure.value

    if(r === 0) {
      emiAmount.value = P / n
    } else {
      // emiAmount.value = (P * r * Math.pow(1 + r, n)) / (Math.pow(1 + r, n) - 1)
      emiAmount.value = P / n + r
    }

    // Total EMI (Compound + Interest)
    emiAmount.value = emiAmount.value.toFixed(2) 

    // Interest Amount per month
    interest_amount_permonth.value = r
  }

</script>

<style>

</style>