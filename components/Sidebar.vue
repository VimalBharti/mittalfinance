<template>
      <aside class="bg-gray-100 w-1/5 h-full">
          <header class="logo border-b border-gray-100 shadow-sm h-20 font-bold text-gray-900 text-center flex items-center  gap-3 px-4">
              <Icon name="material-symbols:home-app-logo" class="w-12 h-12 text-gray-700" />
              <span class="text-xl">Mittal Finance</span>
          </header>
          <nav class="flex flex-col text-gray-500 py-6">
              <NuxtLink to="/dashboard" class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="duo-icons:dashboard" class="w-5 h-5 text-gray-700" />
                  Dashboard
              </NuxtLink>

              <NuxtLink to="/months" class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="material-symbols:calendar-month" class="w-5 h-5 text-gray-700" />
                  Months
              </NuxtLink>

              <!-- Payments -->
              <NuxtLink class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="streamline:bag-rupee" class="w-5 h-5 text-gray-700" />
                  Loans
              </NuxtLink>
                <div class="nested-link">
                    <NuxtLink to="/loans/new" class="py-3 px-6 flex items-center gap-2 text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-600 sidebar-link">
                        <Icon name="hugeicons:save-money-dollar" class="w-5 h-5" />
                        Add New Loan
                    </NuxtLink>
                    <NuxtLink to="/loans" class="py-3 px-6 flex items-center gap-2 text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-600 sidebar-link">
                        <Icon name="tabler:receipt-rupee" class="w-5 h-5" />
                        Loan History
                    </NuxtLink>
                    <NuxtLink to="/loans/emi-entry" class="py-3 px-6 flex items-center gap-2 text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-600 sidebar-link">
                        <Icon name="hugeicons:bubble-chat-delay" class="w-5 h-5" />
                        EMI Entries
                    </NuxtLink>
                </div>

              <!-- Clients -->
              <NuxtLink class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="solar:users-group-rounded-line-duotone" class="w-5 h-5 text-gray-700" />
                  Clients
              </NuxtLink>
                <div class="nested-link">
                    <NuxtLink to="/all-client" class="py-3 px-6 flex items-center gap-2 text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-600 sidebar-link">
                        <Icon name="ph:user-list-duotone" class="w-5 h-5" />
                        All Clients
                    </NuxtLink>
                    <NuxtLink to="/add-client" class="py-3 px-6 flex items-center gap-2 text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-600 sidebar-link">
                        <Icon name="mdi:account-plus-outline" class="w-5 h-5" />
                        Add New Client
                    </NuxtLink>
                </div>

              <NuxtLink to="/" class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="solar:document-add-line-duotone" class="w-5 h-5 text-gray-700" />
                  Documents
              </NuxtLink>

              <NuxtLink to="/reset-setting" class="py-3 px-6 flex items-center gap-2 text-sm hover:bg-gray-200 sidebar-link">
                  <Icon name="mdi:lock-reset" class="w-5 h-5 text-gray-700" />
                  Reset Setting
              </NuxtLink>
          </nav>
      </aside>
  </template>
  
  <script lang="ts" setup>
  
  </script>
  
<style>
  .nested-link{
    margin-left: 32px;
    border-left: 1px solid #dcdcdc;
  }
    .sidebar-link.router-link-active {
        @apply border-l-4 border-gray-900 text-gray-800;
    }
    .sidebar-link.router-link-active:hover {
        @apply border-l-4 border-gray-900 text-gray-800;
    }
</style>