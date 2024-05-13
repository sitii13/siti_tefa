<template>
    <div>
        <canvas id="myChart"></canvas>
    </div>
</template>

<script setup>
import Chart from 'chart.js/auto'


const labels = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'June',
];


const data = {
    labels: labels,
    datasets: [{
    label: 'My First dataset',
    backgroundColor: 'rgb(220, 220, 220)',
    borderColor: 'rgb(2555, 99, 132)',
    data: [10, 20, 25, 20, 20, 25, 45],
    }]
};


const config = {
    type: 'bar',
    data: data,
    options: {}
};
onMounted(() => {
    const myChart = new Chart(
    document.getElementById('myChart'),
    config
    );
})
</script>


