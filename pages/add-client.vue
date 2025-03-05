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

    <div class="grid grid-cols-12 gap-6 p-6">
      
      <div class="w-full col-span-4">
        <div class="bg-white rounded-xl shadow p-4 sm:p-7 dark:bg-neutral-800">
          <div class="mb-8">
            <h2 class="text-xl font-bold text-gray-800">
              KYC Information
            </h2>
            <p class="text-sm text-gray-500">
              Manage client photo
            </p>
          </div>

          <!-- Photo -->
          <div class="w-full">

            <div class="flex flex-col items-center gap-5">
              <img class="inline-block w-40 h-40 rounded-2xl ring-2 ring-white dark:ring-neutral-900" :src="imageUrl ? imageUrl : 'https://preline.co/assets/img/160x160/img1.jpg'" alt="Avatar">
              <div class="flex gap-x-2">
                <UInput type="file" @change="handleFileChange" icon="i-heroicons-folder" />
                <button @click="uploadImage" :disabled="isUploading" class="w-[50px] h-8 bg-gray-700 text-white rounded">
                  <Icon name="line-md:uploading-loop" v-if="isUploading" />
                  <Icon name="material-symbols:upload-rounded" v-else />
                </button>
              </div>
            </div>

          </div>
        </div>
      </div>

      <div class="w-full col-span-8">
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

        </div>
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

  const isSaving = ref(false)
  const saveBtnColor = ref('cyan')

  const fname = ref('');
  const lname = ref('');
  const email = ref('');
  const phone = ref('');
  const gender = ref('');
  const address = ref('');

  const imageFile = ref(null)
  const imageUrl = ref('https://hozukjgrfvcuvdtakkte.supabase.co/storage/v1/object/public/website/avatar/avatar.jpg')
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
          fname : fname.value,
          lname : lname.value,
          fullName : fname.value + ' ' + lname.value,
          email : email.value,
          phone : phone.value,
          gender : gender.value,
          address : address.value,
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
      imageUrl.value = '';

  }


</script>

<style>

</style>