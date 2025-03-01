<template>
  <div class="w-full h-full overflow-y-auto">

    <header class="flex items-center justify-between border-b border-gray-100 shadow-sm h-20 px-6">
      <div class="w-full">
        <h2 class="text-2xl text-gray-700">Dashboard</h2>
        <p class="text-gray-400 text-sm">Good to see you here</p>
      </div>
    </header>

    <!-- Current Status -->
    <!-- <div class="grid grid-cols-2 gap-5 mt-12 mb-5">
        <section class="border rounded-xl p-5">
            <h3 class="font-bold text-gray-700 uppercase text-sm">Clients</h3>
            <ul class="w-full flex flex-col bg-white mt-2">
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    ABC
                </li>
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    DEF
                </li>
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    GHI
                </li>
            </ul>
        </section>
        <section class="border rounded-xl p-5">
            <h3 class="font-bold text-gray-700 uppercase text-sm">Payments</h3>
            <ul class="w-full flex flex-col bg-white mt-2">
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    3000
                </li>
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    2000
                </li>
                <li class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white border border-gray-200 text-gray-800 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg">
                    1200
                </li>
            </ul>
        </section>
    </div> -->
    
    <div class="grid grid-cols-3 gap-5 p-6">
        <section 
            class="rounded-xl p-8 text-gray-800" 
            :style="{'background-color':bgColors[0]}"
        >
            <h2 class="text-3xl font-bold">{{ currentMonth.name }}</h2>
            <h3>{{ currentCount }} Clients</h3>
            <NuxtLink :to="`/${year}/${monthNumber}`" class="text-right w-full flex items-center justify-end gap-1 mt-4 group text-xs uppercase">
                <span class="group-hover:font-bold group-hover:border-b border-gray-800">View all</span>
                <Icon name="material-symbols:arrow-right-alt" class="w-5 h-5 group-hover:scale-150 transition duration-700 ease-in-out" />
            </NuxtLink>
        </section>
        <section 
            class="rounded-xl p-8 text-gray-800" 
            :style="{'background-color':bgColors[1]}"
        >
            <h2 class="text-3xl font-bold">{{ secondMonth.name }}</h2>
            <h3>{{ secondMonthCount }} Clients</h3>
            <NuxtLink :to="`/${year}/${secondMonthNumber}`" class="text-right w-full flex items-center justify-end gap-1 mt-4 group text-xs uppercase">
                <span class="group-hover:font-bold group-hover:border-b border-gray-800">View all</span>
                <Icon name="material-symbols:arrow-right-alt" class="w-5 h-5 group-hover:scale-150 transition duration-700 ease-in-out" />
            </NuxtLink>
        </section>
        <section 
            class="rounded-xl p-8 text-gray-800" 
            :style="{'background-color':bgColors[2]}"
        >
            <h2 class="text-3xl font-bold">{{ thirdMonth.name }}</h2>
            <h3>{{ thirdMonthCount }} Clients</h3>
            <NuxtLink :to="`/${year}/${thirdMonthNumber}`" class="text-right w-full flex items-center justify-end gap-1 mt-4 group text-xs uppercase">
                <span class="group-hover:font-bold group-hover:border-b border-gray-800">View all</span>
                <Icon name="material-symbols:arrow-right-alt" class="w-5 h-5 group-hover:scale-150 transition duration-700 ease-in-out" />
            </NuxtLink>
        </section>
    </div>

    <div class="grid grid-cols-2 gap-5 px-6">
        <section class="grid grid-cols-2 gap-5">
            <div class="flex justify-between border rounded-xl p-5" v-for="quick in quicks" :key="quick">
                <div class="space-y-3">
                    <h4 class="text-gray-400 text-sm">{{ quick.title }}</h4>
                    <h3 class="text-2xl font-bold text-gray-800">{{ quick.value }}</h3>
                </div>
                <button class="border rounded-full w-10 h-10  text-gray-800 flex items-center justify-center">
                    <Icon :name="quick.icon" class="w-5 h-5" /></button>
            </div>
        </section>
        <section>
            <div class="bg-gray-900 rounded-xl p-5 h-full">
                <div class="flex justify-between rounded-xl p-5">
                    <div class="space-y-3">
                        <h4 class="text-gray-300 text-sm">Monthly Revenue</h4>
                        <h3 class="text-2xl font-bold text-gray-100">50,000</h3>
                    </div>
                    <button class="border border-gray-400 rounded-full w-16 h-16  text-gray-400 flex items-center justify-center">
                        <Icon name="material-symbols-light:bar-chart-4-bars-rounded" class="w-8 h-8" />
                    </button>
                </div>
                <BarChart />
            </div>
        </section>
    </div>
  </div>
</template>

<script setup>
    definePageMeta({
        layout: 'dashboard'
    })

    const supabase = useSupabaseClient()

    const totalLoanAmount = ref(0)

    const quicks = [
        { title: 'Total Loan Amount', value: totalLoanAmount, icon: 'material-symbols:currency-rupee' },
        { title: 'Total Clients', value: '300', icon: 'solar:users-group-rounded-linear' },
        { title: 'Documents', value: '240', icon: 'material-symbols:file-copy-outline' },
        { title: 'Defaulters ', value: '12', icon: 'streamline:interface-user-block-actions-block-close-denied-deny-geometric-human-person-single-up-user' },
    ]

    const currentDate = new Date()
    const year = currentDate.getFullYear()

    const monthNumber  = String(currentDate.getMonth() + 1).padStart(2, '0')
    const secondMonthNumber = String(currentDate.getMonth() + 2).padStart(2, '0') // Next Month
    const thirdMonthNumber = String(currentDate.getMonth() + 3).padStart(2, '0') // Next Month

    const months = [
        { number: '01', name: 'January' },
        { number: '02', name: 'February' },
        { number: '03', name: 'March' },
        { number: '04', name: 'April' },
        { number: '05', name: 'May' },
        { number: '06', name: 'June' },
        { number: '07', name: 'July' },
        { number: '08', name: 'August' },
        { number: '09', name: 'September' },
        { number: '10', name: 'October' },
        { number: '11', name: 'November' },
        { number: '12', name: 'December' }
    ]

    const currentCount = ref(0)
    const secondMonthCount = ref(0)
    const thirdMonthCount = ref(0)

    const currentMonth = months.find(m => m.number === monthNumber)
    const secondMonth = months.find(m => m.number === secondMonthNumber)
    const thirdMonth = months.find(m => m.number === thirdMonthNumber)

    const bgColors = ref(['oklch(0.945 0.129 101.54)', 'oklch(0.967 0.001 286.375)', 'oklch(0.827 0.119 306.383)'])

    const fetchTotalLoanAmount = async () => {
        const { data, error } = await supabase
            .from('clients')
            .select('loanAmount')

        if (error) {
            console.error('Error fetching loan amount:', error)
            return
        }

        // Calculate sum of "loan_amount"
        totalLoanAmount.value = data.reduce((sum, record) => sum + (record.loanAmount || 0), 0)
    }

    const fetchCurrentMonth = async () => {
        const startDate = `${year}-${monthNumber}-01`
        const endDate = new Date(year, monthNumber, 0).toISOString().split('T')[0]  // Last day of the month
        
        const { count: total, error } = await supabase
            .from('clients')
            .select('*', { count: 'exact', head: true }) // Get count without fetching data
            .gte('salaryCreditDate', startDate)
            .lte('salaryCreditDate', endDate)

        if (error) {
            console.error('Error fetching data:', error)
        } else {
            currentCount.value = total
        }
    }
    const fetchSecondMonth = async () => {
        const startDate = `${year}-${secondMonthNumber}-01`
        const endDate = new Date(year, secondMonthNumber, 0).toISOString().split('T')[0]  // Last day of the month
        
        const { count: total, error } = await supabase
            .from('clients')
            .select('*', { count: 'exact', head: true }) // Get count without fetching data
            .gte('salaryCreditDate', startDate)
            .lte('salaryCreditDate', endDate)

        if (error) {
            console.error('Error fetching data:', error)
        } else {
            secondMonthCount.value = total
        }
    }
    const fetchThirdMonth = async () => {
        const startDate = `${year}-${thirdMonthNumber}-01`
        const endDate = new Date(year, thirdMonthNumber, 0).toISOString().split('T')[0]  // Last day of the month
        
        const { count: total, error } = await supabase
            .from('clients')
            .select('*', { count: 'exact', head: true }) // Get count without fetching data
            .gte('salaryCreditDate', startDate)
            .lte('salaryCreditDate', endDate)

        if (error) {
            console.error('Error fetching data:', error)
        } else {
            thirdMonthCount.value = total
        }
    }
    onMounted(
        fetchCurrentMonth(), 
        fetchSecondMonth(), 
        fetchThirdMonth(), 
        fetchTotalLoanAmount()
    )

</script>

<style>

</style>