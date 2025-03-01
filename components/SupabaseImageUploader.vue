<script setup>
const supabase = useSupabaseClient()

const props = defineProps({
  bucket: { type: String, required: true }, // Bucket name
  folder: { type: String, default: '' }, // Optional folder structure
  onUpload: { type: Function, default: null } // Callback function after upload
})

const file = ref(null)
const imageUrl = ref(null)
const uploading = ref(false)

const handleFileChange = (event) => {
  file.value = event.target.files[0]
}

const uploadImage = async () => {
  if (!file.value) return alert('Please select a file')

  uploading.value = true

  const fileName = `${props.folder}${Date.now()}-${file.value.name}`
  const { data, error } = await supabase.storage.from(props.bucket).upload(fileName, file.value)

  if (error) {
    alert('Upload failed: ' + error.message)
  } else {
    // Get public URL
    const { data: publicUrl } = supabase.storage.from(props.bucket).getPublicUrl(fileName)
    imageUrl.value = publicUrl.publicUrl

    // Emit the uploaded URL
    if (props.onUpload) props.onUpload(imageUrl.value)
  }

  uploading.value = false
}
</script>

<template>
  <div class="p-4 border rounded w-[600px] flex gap-8">
    <input type="file" @change="handleFileChange" accept="image/*" class="mb-2 w-full" />
    <button @click="uploadImage" :disabled="uploading" class="bg-blue-500 text-white px-4 py-2 rounded">
      {{ uploading ? 'Uploading...' : 'Upload Image' }}
    </button>

    <div v-if="imageUrl" class="mt-4">
      <p>Uploaded Image:</p>
      <img :src="imageUrl" alt="Uploaded Image" class="w-40 h-40 object-cover border rounded" />
    </div>
  </div>
</template>
