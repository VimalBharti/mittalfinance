<template>
  <div class="w-full h-full overflow-y-auto">
    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">New Client</h2>
        <p class="text-gray-400 text-sm">add new client to list</p>
      </div>
      <UButton :loading="isSaving" :color="saveBtnColor" @click="addNewClient" class="px-4 py-2">Save Details</UButton>
    </header>
    <UProgress animation="carousel" size="sm" color="cyan" v-if="isSaving" />

    <div class="grid grid-cols-2 gap-6 p-6">
      <div class="w-full"><!-- Card -->
        <div class="bg-white rounded-xl shadow p-4 sm:p-7 dark:bg-neutral-800">
          <div class="mb-8">
            <h2 class="text-xl font-bold text-gray-800">
              Basic Details
            </h2>
            <p class="text-sm text-gray-500">
              Manage client name, contact, address etc.
            </p>
          </div>

            <!-- Grid -->
            <div class="grid sm:grid-cols-12 gap-2 sm:gap-6">

              <!-- Serial Number -->
              <!-- <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Serial number
                </label>
              </div>
              <div class="sm:col-span-9 flex items-center ">
                <div class="text-sm bg-gray-50 py-2 px-5 rounded-lg text-gray-500">{{serialnumber}}</div>
              </div> -->


              <!-- Profile Photo -->
              <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Client photo
                </label>
              </div>
              <div class="sm:col-span-9">
                <div class="flex items-center gap-5">
                  <img class="inline-block size-16 rounded-full ring-2 ring-white dark:ring-neutral-900" :src="imageUrl ? imageUrl : 'https://preline.co/assets/img/160x160/img1.jpg'" alt="Avatar">
                  <div class="flex gap-x-2">
                    <UInput type="file" @change="handleFileChange" icon="i-heroicons-folder" />
                    <button @click="uploadImage" :disabled="isUploading" class="w-[50px] h-8 bg-gray-700 text-white rounded">
                      <Icon name="line-md:uploading-loop" v-if="isUploading" />
                      <Icon name="material-symbols:upload-rounded" v-else />
                    </button>
                  </div>
                </div>
              </div>
              <!-- End Col -->

              <!-- <SupabaseImageUploader bucket="website" folder="avatar/" :onUpload="handleImageUpload" class="" /> -->

              <!-- Full Name -->
              <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Full name
                </label>
              </div>
              <div class="sm:col-span-9">
                <div class="sm:flex">
                  <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="Vimal" v-model="fname">
                  <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="Bharti" v-model="lname">
                </div>
              </div>

              <!-- Email -->
              <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Email
                </label>
              </div>
              <div class="sm:col-span-9">
                <input type="email" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="vimal@site.com" v-model="email">
              </div>

              <!-- Phone number -->
              <div class="sm:col-span-3">
                <div class="inline-block">
                  <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                    Phone
                  </label>
                  <!-- <span class="text-sm text-gray-400 dark:text-neutral-600">
                    (Optional)
                  </span> -->
                </div>
              </div>
              <div class="sm:col-span-9">
                <div class="sm:flex">
                  <!-- <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="+x(xxx)xxx-xx-xx" v-model="phone"> -->
                  <UInput
                    v-model="phone"
                    maxlength="10"
                    class="w-full"
                  >
                    <template #leading>
                      <span class="text-gray-500 dark:text-gray-400 text-xs">+91</span>
                    </template>
                    <template #trailing>
                      <span class="text-xs text-gray-500 dark:text-gray-400">{{ phone.length }}/10</span>
                    </template>
                  </UInput>
                </div>
              </div>

              <!-- Gender -->
              <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Gender
                </label>
              </div>
              <div class="sm:col-span-9">
                <div class="sm:flex">
                  <label class="flex py-2 px-3 w-full border border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none">
                    <input type="radio" name="af-account-gender-checkbox" class="shrink-0 mt-0.5 border-gray-300 rounded-full text-blue-600 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-neutral-800 dark:border-neutral-500 dark:checked:bg-blue-500 dark:checked:border-blue-500 dark:focus:ring-offset-gray-800" checked v-model="gender">
                    <span class="text-sm text-gray-500 ms-3 dark:text-neutral-400">Male</span>
                  </label>

                  <label class="flex py-2 px-3 w-full border border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none">
                    <input type="radio" name="af-account-gender-checkbox" class="shrink-0 mt-0.5 border-gray-300 rounded-full text-blue-600 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-neutral-800 dark:border-neutral-500 dark:checked:bg-blue-500 dark:checked:border-blue-500 dark:focus:ring-offset-gray-800" v-model="gender">
                    <span class="text-sm text-gray-500 ms-3 dark:text-neutral-400">Female</span>
                  </label>
                </div>
              </div>

              <!-- Address -->
              <div class="sm:col-span-3">
                <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                  Address
                </label>
              </div>
              <div class="sm:col-span-9">
                <textarea class="py-2 px-3 block w-full border border-gray-200 rounded-lg text-sm focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" rows="6" placeholder="client address..." v-model="address"></textarea>
              </div>

            </div>
            <!-- End Grid -->

            <section class="bg-white mt-8 border-t pt-6">
              <div class="mb-8">
                <h2 class="text-xl font-bold text-gray-800">
                  KYC Information
                </h2>
                <p class="text-xs text-gray-500">
                  Client Photo with documents
                </p>
              </div>

              <div class="w-full">

                <div class="flex item-center gap-5 justify-between">
                  <label for="af-account-email" class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                    Upload Photo
                  </label>
                  <UInput type="file" size="sm" icon="i-heroicons-folder" class="w-auto" />
                </div>
                <!-- End Col -->

              </div>
            </section>
        </div>
      </div>

      <!-- Loan Details Section -->
      <div class="w-full">
        <section class="bg-white rounded-xl shadow p-4 sm:p-7 dark:bg-neutral-800">
          <div class="mb-8">
            <h2 class="text-xl font-bold text-gray-800">
              Loan Details
            </h2>
            <p class="text-sm text-gray-500">
              Manage loan amount, tenure, interest, docs etc.
            </p>
          </div>

          <!-- Grid -->
          <div class="grid sm:grid-cols-12 gap-2 sm:gap-6">

            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Loan Amount
              </label>
            </div>
            <div class="sm:col-span-9">
              <input type="text" class="py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none" placeholder="10,000" v-model="loanAmount" @input="calculateEMI">
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
            <div class="sm:col-span-3">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                EMI Amount
              </label>
            </div>
            <div class="sm:col-span-9">
              <input type="text" class="py-2 px-3 pe-11 block w-full border border-gray-200 shadow-sm text-sm rounded-lg focus:border-gray-500 focus:ring-gray-500 disabled:opacity-50 disabled:pointer-events-none bg-gray-100" placeholder="5,000" v-model="emiAmount">
            </div>
            <!-- End Col -->

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

        <section class="bg-white rounded-xl shadow p-4 sm:p-7 mt-5">
          <div class="mb-8">
            <h2 class="text-xl font-bold text-gray-800">
              Documents
            </h2>
            <p class="text-sm text-gray-500">
              Adhaar card, PAN card, ATM etc.
            </p>
          </div>

          <div class="w-full">

            <div class="flex item-center gap-5 justify-between">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                Adhaar Card
              </label>
              <UInput type="file" size="sm" icon="i-heroicons-folder" class="w-auto" />
            </div>
            <!-- End Col -->

            <!-- PAN Card -->
            <div class="flex item-center gap-5 justify-between mt-6">
              <label class="inline-block text-sm text-gray-800 mt-2.5 dark:text-neutral-200">
                PAN Card
              </label>
              <UInput type="file" size="sm" icon="i-heroicons-folder" class="w-auto" />
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

  const tenures = [6, 10, 12, 24];
  const percentage = [2, 3, 5, 7];
  const date = ref(new Date())

  const isSaving = ref(false)
  const saveBtnColor = ref('cyan')

  const generateSerial = (prefix = 'MITFIN') => {
    const now = new Date()
    return `${prefix}-${now.getFullYear()}${Math.floor(1000 + Math.random() * 9000)}`
  }

  const fname = ref('');
  const lname = ref('');
  const email = ref('');
  const phone = ref('');
  const gender = ref('');
  const address = ref('');
  const loanAmount = ref();
  const interestRate = ref() //Annual interest rate (in %);
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

  const addNewClient = async () => {
    isSaving.value = true;
    saveBtnColor.value = 'gray';

    const { data, error } = await supabase
      .from('clients')
      .insert([
        { 
          serialnumber: serialnumber.value,
          fname : fname.value,
          lname : lname.value,
          fullName : fname.value + '' + lname.value,
          email : email.value,
          phone : phone.value,
          gender : gender.value,
          address : address.value,
          loanAmount : loanAmount.value,
          interestRate : interestRate.value,
          loanTenure : loanTenure.value,
          emiAmount : emiAmount.value,
          emiStartDate : emiStartDate.value,
          lastEmiDate : lastEmiDate.value,
          salaryCreditDate : date.value,
          photo : imageUrl.value
        },
      ])
      .select()

      isSaving.value = false;
      saveBtnColor.value = 'cyan';

      // Reset values
      fname.value = '';
      lname.value = '';
      email.value = '';
      phone.value = '';
      gender.value = '';
      address.value = '';
      loanAmount.value = '';
      interestRate.value = ''
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

    emiAmount.value = emiAmount.value.toFixed(2) 
  }

</script>

<style>

</style>