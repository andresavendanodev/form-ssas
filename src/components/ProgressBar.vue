<template>
    <div class="h-4 relative rounded-full overflow-hidden">
        <div class="w-full h-full bg-gray-200 absolute"></div>
        <div class="h-full bg-indigo-500 absolute" :style="{ width: width }"></div>
        <div v-for="step in steps">
            <div class="w-4 h-4 bg-white border-2 border-indigo-500 absolute rounded-full" :style="{ left: step.position }"
                :class="{ 'bg-indigo-500': step.completed }"></div>
        </div>
    </div>
</template>


<script>
export default {
    name: 'ProgressBar',
    props: {
        currentStep: {
            type: Number,
            required: true,
        },
        totalSteps: {
            type: Number,
            required: true,
        },
    },
    computed: {
        steps() {
            const steps = []
            for (let i = 1; i <= this.totalSteps; i++) {
                steps.push({
                    position: `${((i - 1) * 100) / (this.totalSteps - 1)}%`,
                    completed: i <= this.currentStep,
                })
            }
            return steps
        },
        width() {
            return `${((this.currentStep - 1) * 100) / (this.totalSteps - 1)}%`
        },
    },
}
</script> 
