<template>
  <div class="bg-pattern h-screen relative">
    <!-- Floating Icons -->
    <button class="absolute -top-16 -left-16 text-gray-200 border rounded-full w-36 h-36">
      <Icon name="material-symbols:finance-mode" class="w-20 h-20" />
    </button>
    <button class="absolute top-[35%] left-0 text-gray-200 border rounded-full w-40 h-40">
      <Icon name="material-symbols:finance-mode" class="w-28 h-28" />
    </button>
    <button class="absolute bottom-2 left-0 text-gray-200 border rounded-full w-36 h-36">
      <Icon name="streamline:money-cash-bag-dollar-bag-payment-cash-money-finance" class="w-20 h-20" />
    </button>
    <button class="absolute bottom-10 right-0 text-gray-200 border rounded-full w-36 h-36">
      <Icon name="streamline:money-cash-coins-stack-accounting-billing-payment-stack-cash-coins-currency-money-finance" class="w-20 h-20" />
    </button>
    <button class="absolute top-10 right-10 text-gray-200 border rounded-full w-36 h-36">
      <Icon name="heroicons:banknotes" class="w-20 h-20" />
    </button>

    <div class="w-full h-full flex flex-col justify-between items-center py-6 max-w-5xl mx-auto text-gray-900">
      <h2 class=" font-bold shadow-xl rounded-xl px-5 py-3 border">Mittal Finance</h2>
      <div class="text-[15vh] font-bold text-center leading-none">
        One of the <br/> most effective <br/> financial tool
      </div>
      <div class="flex items-center justify-between gap-20 max-w-3xl mx-auto border rounded-3xl p-4 shadow-xl">
        <div>
          <h3 class="font-bold">Mittal Finanace Loan</h3>
          <p class="text-sm">By purchasing coins you can earn good money with tools such as staking and bond.</p>
        </div>
        <NuxtLink to="/dashboard" class="text-white bg-gray-900 px-8 py-3 rounded-3xl w-[200px] hover:bg-white hover:text-gray-900 hover:border-2 hover:border-gray-800 cursor-pointer text-center">Enter to APP</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>

</script>

<style scoped>
.bg-pattern{
  background-color: #ffffff;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='4' height='4' viewBox='0 0 4 4'%3E%3Cpath fill='%23d2d2d2' fill-opacity='0.5' d='M1 3h1v1H1V3zm2-2h1v1H3V1z'%3E%3C/path%3E%3C/svg%3E");
}
</style>