<template>
    <div class="pie-container">
        <p class="pie-last-time">{{ lastvalueTime }}</p>
        <canvas id="pieVoltage"></canvas>
        <div class="pie-value pie-voltage">{{ value }}<p>вольт</p>
        </div>
        <div class="sample-value">
            <div>0</div>
            <div>300</div>
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
        let ctx = document.getElementById('pieVoltage');
        let lastvalue = this.controllerInfoStorage;

        if (lastvalue.status === null) {
            if (this.lastResult[0] !== undefined) {
                this.lastvalueTime = this.lastResult[0].created_at;
                this.value = this.lastResult[0].load_A_v;
            }
        } else {
            let dateTitle = lastvalue.status.created_at.split(',');
            this.lastvalueTime = dateTitle[0] + ' ' + dateTitle[1].slice(0, -3);
            this.value = lastvalue.status.load_A_v;
        }

        // 0 - 300 вольт

        let a = this.value;
        let b = 300 - a;
        let c = 300;

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
                    '#fefefe',
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

<style>
#pieVoltage,
#bat_cChart {
    transform: rotate(-90deg);
}

.sample-value {
    position: absolute;
    padding: 0 24px;
    font-size: 14px;
    width: 84%;
    top: 56%;
    display: flex;
    justify-content: space-between;
}

.sample-value div {
    width: 30px;
    text-align: center;
}

@media (min-width: 1600px) {
    .sample-value div {
        width: 36px;
    }

    .sample-value {
        font-size: 14px;
    }
}

@media (min-width: 1700px) {
    .sample-value div {
        width: 43px;
    }
}

@media (min-width: 1900px) {
    .sample-value div {
        width: 106px;
        font-size: 16px;
    }
}

@media (min-width: 2200px) {
    .sample-value div {
        width: 170px;
        font-size: 16px;
    }
}

@media (min-width: 2500px) {
    .sample-value div {
        width: 190px;
        font-size: 20px;
    }
}
</style>