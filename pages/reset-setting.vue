<template>
  <div class="w-full h-full overflow-y-auto relative">
    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">Reset Settings</h2>
        <p class="text-gray-400 text-sm">Reset monthly status, delete clients etc.</p>
      </div>
      <!-- <NuxtLink to="/add-client" class="border border-gray-900 text-gray-900 px-4 py-3 rounded-xl w-40 text-sm text-center">Add Loan</NuxtLink> -->
    </header>

    <div class="w-full p-8">
      <div class="grid grid-cols-3 gap-5">
        <UCard>
          <div>
            <h2>Reset Monthly Status</h2>
            <p class="text-sm text-gray-400 mt-2">All loan Monthly status set to <span class="font-bold text-red-600">"FALSE"</span></p>
          </div>
          <template #footer>
            <button class="w-full bg-gray-700 text-white rounded-lg text-sm p-3" @click="updateMonthlyStatus">Reset Now</button>
          </template>
        </UCard>
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
  const toast = useToast()

  // Reset MOnthly EMI Status
  const updateMonthlyStatus = async () => {
    const {error} = await supabase
      .from('loans')
      .update({ emi_monthly_status: false })
      .neq("id", 0)

    if (error) {
      console.error("Error updating status:", error)
    } else {
      toast.add({
        id: 'update_downloaded',
        title: 'Reset Succefully',
        description: 'Loan monthly status set to FALSE',
        icon: 'hugeicons:task-done-01',
      })
    }
  }
</script>

<style>

</style>