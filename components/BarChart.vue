<template>
  <Bar
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
  />
</template>

<script lang="ts" setup>
    import { Bar } from 'vue-chartjs'
    import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

    ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

    const chartData = {
        labels: [ 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        datasets: [ 
            { 
                label: 'Revenue(in thousands)',
                backgroundColor: '#f87979',
                data: [40, 20, 12,40, 20, 12,40, 20, 12, 32, 55, 66] 
            } 
        ]
    }

    const chartOptions = {
        responsive: true
    }
</script>

<style>

</style>