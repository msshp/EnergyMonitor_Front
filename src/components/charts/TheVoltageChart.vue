<template>
    <canvas id="voltageChart"></canvas>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
    props: {
        controllerInfoStorage: Array,
    },
    mounted() {
        let ctx = document.getElementById('voltageChart');

        let labels = [];
        let dataPvV = [];
        let dataBatV = [];
        let dataLoadV = [];

        console.log(this.controllerInfoStorage)
        this.controllerInfoStorage.forEach((el) => {
            labels.push(el.created_at);
            dataPvV.push(el.load_A_v);
            dataBatV.push(el.load_B_v);
            dataLoadV.push(el.load_C_v);
        });

        labels.reverse();
        dataPvV.reverse();
        dataBatV.reverse();
        dataLoadV.reverse();

        new Chart(ctx, {
            type: 'line',
            data: {
                labels: labels,
                datasets: [
                    {
                        label: 'Напряжение канал А (В)',
                        data: dataPvV,
                        borderWidth: 2,
                        borderColor: '#F4CA8D',
                        pointBorderWidth: 0,
                        pointHitRadius: 0,
                        cubicInterpolationMode: 'monotone',
                        pointStyle: 'cross',
                        backgroundColor: '#F4CA8D',
                    },
                    {
                        label: 'Напряжение канал B',
                        data: dataBatV,
                        borderWidth: 2,
                        borderColor: '#B6DE14',
                        pointBorderWidth: 0,
                        pointHitRadius: 0,
                        cubicInterpolationMode: 'monotone',
                        pointStyle: 'cross',
                        backgroundColor: '#B6DE14',
                    },
                    {
                        label: 'Напряжение канал C',
                        data: dataLoadV,
                        borderWidth: 2,
                        borderColor: '#B6DE14',
                        pointBorderWidth: 0,
                        pointHitRadius: 0,
                        cubicInterpolationMode: 'monotone',
                        pointStyle: 'cross',
                        backgroundColor: '#B6DE14',
                    }
                ]
            },
            options: {
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });
    }
}

</script>