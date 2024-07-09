<script setup>
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});
</script>

<script>
export default {
    data() {
        return {
            salary: 0,
            formatLang: 'en-EN',
            formatStyle: 'currency',
            formatCurrency: 'GBP'
        }
    },
    computed: {
        formatter() {
            return new Intl.NumberFormat(this.formatLang, {
                style: this.formatStyle,
                currency: this.formatCurrency
            })
        },
        formattedCostYear() {
            return this.formatter.format(this.salary)
        },
        formattedCostMonth() {
            return this.formatter.format(this.salary / 12)
        },
        formattedCostWeek() {
            return this.formatter.format(this.salary / 52)
        },
        incomeTaxYear(){
            return this.formatter.format((this.salary / 100) * 11)
        },
        incomeTaxMonth(){
            return this.formatter.format((this.salary / 100) * 11 / 12)
        },
        incomeTaxDay(){
            return this.formatter.format((this.salary / 100) * 11 / 52)
        },
        nationalInsuranceYear(){
            return this.formatter.format((this.salary / 100) * 5.5)
        },
        nationalInsuranceMonth(){
            return this.formatter.format((this.salary / 100) * 5.5 / 12 )
        },
        nationalInsuranceDay(){
            return this.formatter.format((this.salary / 100) * 5.5 / 52 )
        },
        takeHomePayYear(){
            return this.formatter.format(this.salary - (this.salary / 100) * 11 - (this.salary / 100) * 5.5)
        },
        takeHomePayMonth(){
            return this.formatter.format((this.salary / 12) - (this.salary / 100) * 11 / 12 - (this.salary / 100) * 5.5 / 12)
        },
        takeHomePayDay(){
            return this.formatter.format((this.salary / 52) - (this.salary / 100) * 11 / 52 - (this.salary / 100) * 5.5 / 52)
        },
    }
}
</script>

<template>
    <Head title="Tax Calculator" />

    <div class="flex justify-center py-16 text-sm text-black dark:text-white/70">
        <div class="text-center">
            <h1>Enter your salary</h1>
            <input type="number" v-model="salary">
        </div>
    </div>
    <div class="flex justify-center py-16 text-sm text-black">
        <table class="border-separate border-spacing-x-16 border-spacing-y-4 border border-slate-400">
            <thead>
                <tr>
                    <th></th>
                    <th>Yearly</th>
                    <th>Monthly</th>
                    <th>Weekly</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Gross salary</td>
                    <td>{{ formattedCostYear }}</td>
                    <td>{{ formattedCostMonth }}</td>
                    <td>{{ formattedCostWeek }}</td>
                </tr>
                <tr>
                    <td>Income Tax</td>
                    <td>{{ incomeTaxYear }}</td>
                    <td>{{ incomeTaxMonth }}</td>
                    <td>{{ incomeTaxDay }}</td>
                </tr>
                <tr>
                    <td>National Insurance</td>
                    <td>{{ nationalInsuranceYear }}</td>
                    <td>{{ nationalInsuranceMonth }}</td>
                    <td>{{ nationalInsuranceDay }}</td>
                </tr>
                <tr>
                    <td>Take home pay</td>
                    <td>{{ takeHomePayYear }}</td>
                    <td>{{ takeHomePayMonth }}</td>
                    <td>{{ takeHomePayDay }}</td>
                </tr>
            </tbody>
        </table>
    </div>
    
    <footer class="py-16 text-center text-sm text-black dark:text-white/70">
        Laravel v{{ laravelVersion }} (PHP v{{ phpVersion }})
    </footer>
</template>
