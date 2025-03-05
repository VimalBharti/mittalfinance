<template>
  <div>
    dd
  </div>
</template>

<script setup>
  definePageMeta({
    layout: 'dashboard',
    colorMode: 'light',
  })

  const supabase = useSupabaseClient()
  const route = useRoute()

  const loans = ref([])

  const fetchRecords = async () => {
    isLoading.value = true

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
      isLoading.value = false
    }
  }

  onMounted(fetchRecords)
</script>

<style>

</style>