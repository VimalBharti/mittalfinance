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

    <!-- Loading screen -->
     <!-- <div class="bg-white/50 backdrop-blur-sm fixed top-0 right-0 left-0 bottom-0 flex items-center justify-center">
       <svg xmlns="http://www.w3.org/2000/svg" class="h-36 w-36" viewBox="0 0 200 200"><circle fill="#FF156D" stroke="#FF156D" stroke-width="15" r="15" cx="35" cy="100"><animate attributeName="cx" calcMode="spline" dur="2" values="35;165;165;35;35" keySplines="0 .1 .5 1;0 .1 .5 1;0 .1 .5 1;0 .1 .5 1" repeatCount="indefinite" begin="0"></animate></circle><circle fill="#FF156D" stroke="#FF156D" stroke-width="15" opacity=".8" r="15" cx="35" cy="100"><animate attributeName="cx" calcMode="spline" dur="2" values="35;165;165;35;35" keySplines="0 .1 .5 1;0 .1 .5 1;0 .1 .5 1;0 .1 .5 1" repeatCount="indefinite" begin="0.05"></animate></circle><circle fill="#FF156D" stroke="#FF156D" stroke-width="15" opacity=".6" r="15" cx="35" cy="100"><animate attributeName="cx" calcMode="spline" dur="2" values="35;165;165;35;35" keySplines="0 .1 .5 1;0 .1 .5 1;0 .1 .5 1;0 .1 .5 1" repeatCount="indefinite" begin=".1"></animate></circle><circle fill="#FF156D" stroke="#FF156D" stroke-width="15" opacity=".4" r="15" cx="35" cy="100"><animate attributeName="cx" calcMode="spline" dur="2" values="35;165;165;35;35" keySplines="0 .1 .5 1;0 .1 .5 1;0 .1 .5 1;0 .1 .5 1" repeatCount="indefinite" begin=".15"></animate></circle><circle fill="#FF156D" stroke="#FF156D" stroke-width="15" opacity=".2" r="15" cx="35" cy="100"><animate attributeName="cx" calcMode="spline" dur="2" values="35;165;165;35;35" keySplines="0 .1 .5 1;0 .1 .5 1;0 .1 .5 1;0 .1 .5 1" repeatCount="indefinite" begin=".2"></animate></circle></svg>
    </div> -->
  </div>
</template>

<script setup>
  const router = useRouter();

</script>

<style scoped>
.bg-pattern{
  background-color: #ffffff;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='4' height='4' viewBox='0 0 4 4'%3E%3Cpath fill='%23d2d2d2' fill-opacity='0.5' d='M1 3h1v1H1V3zm2-2h1v1H3V1z'%3E%3C/path%3E%3C/svg%3E");
}
</style>