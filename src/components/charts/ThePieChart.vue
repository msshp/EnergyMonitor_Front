<template>
    <div class="pie-container">
        <p class="pie-last-time">{{ lastvalueTime }}</p>
        <canvas id="bat_cChart"></canvas>
        <div class="pie-value pie-voltage">{{ value }}<p>ампер</p>
        </div>
        <div class="sample-value">
            <div>0</div>
            <div>50</div>
        </div>
    </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
    props: {
        controllerInfoStorage: Object,
        lastResult: Array
    },
    data() {
        return {
            value: null,
            chartColor: '',
            chartDefColor: '#A9B8D7',
            lastvalueTime: ''
        }
    },
    methods: {
        twoDigits(num) {
            return ('0' + num).slice(-2);
        }
    },
    mounted() {

        let ctx = document.getElementById('bat_cChart');
        let lastvalue = this.controllerInfoStorage;

        if (lastvalue.status === null) {
            if (this.lastResult[0] !== undefined) {
                this.lastvalueTime = this.lastResult[0].created_at;
                this.value = this.lastResult[0].load_A_i;
            }
        } else {
            let dateTitle = lastvalue.status.created_at.split(',');
            this.lastvalueTime = dateTitle[0] + ' ' + dateTitle[1].slice(0, -3);
            this.value = lastvalue.status.load_A_i;
        }
        // 0 - 50 А
        let a = this.value;
        let b = 50 - a;
        let c = 50;

        this.chartColor = '#1976d2';

        if (Number(this.value) === 0) {
            this.chartDefColor = '#E94B4B';
        }

        const chartdata = {
            datasets: [{
                data: [a, b, c],
                borderWidth: [0, 0],
                backgroundColor: [
                    this.chartColor,
                    this.chartDefColor,
                    '#fefefe'
                ],
                hoverBackgroundColor: [
                    this.chartColor,
                    this.chartDefColor,
                    '#fefefe'
                ],
                hoverOffset: [3, 0]
            }]
        }

        new Chart(ctx, {
            type: 'doughnut',
            data: chartdata,
            options: {
                cutout: 90,
                plugins: {
                    tooltip: {
                        enabled: false
                    }
                }
            }
        });
    }
}

</script>