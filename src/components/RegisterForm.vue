<template>
    <div class="flex flex-col justify-center items-center h-screen">
        <h1 class="text-4xl font-bold mb-4">Registro</h1>
        <div class="w-3/4">
            <ProgressBar :current-step="currentStep" :total-steps="totalSteps" />
            <div class="mt-8">
                <component :is="currentStepComponent" />
            </div>
            <div class="mt-8 flex justify-between">
                <button v-if="currentStep > 1" @click="previousStep"
                    class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg mr-4">
                    Anterior
                </button>
                <button @click="nextStep" :disabled="!isValidForm" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
                    {{ currentStep === steps.length ? 'Enviar' : 'Siguiente' }}
                </button>
                
            </div>
        </div>
    </div>
</template>

<script>
import ProgressBar from './ProgressBar.vue'
import StepOne from './StepOne.vue'
import StepTwo from './StepTwo.vue'
import StepThree from './StepThree.vue'



export default {
    name: 'RegisterForm',
    components: {
        ProgressBar,
        StepOne,
        StepTwo,
        StepThree,
    },
    data() {
        return {
            currentStep: 1,
            totalSteps: 3,
            steps: [
                {
                    label: 'Paso 1',
                    component: 'StepOne',
                },
                {
                    label: 'Paso 2',
                    component: 'StepTwo',
                },
                {
                    label: 'Paso 3',
                    component: 'StepThree',
                },
            ],
            formData: {},
        }
    },
    computed: {
        currentStepComponent() {
            return this.steps[this.currentStep - 1].component
        },
        isValidForm() {
            // Validar que los campos requeridos estén llenos para habilitar el botón de siguiente
            // implementar esta lógica en los componentes hijos de cada ppaso del formulario
            return true
        },
    },
    methods: {
        nextStep() {
            if (this.currentStep < this.steps.length) {
                this.currentStep++
            } else {
                this.submitForm()
            }
        },
        previousStep() {
            if (this.currentStep > 1) {
                this.currentStep--
            }
        },
        submitForm() {
            console.log(this.formData)
            // this.$refs.modal.open()
        },
    },
}
</script>
