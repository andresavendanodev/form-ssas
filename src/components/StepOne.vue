<template>
    <div class="grid gap-4 grid-cols-3 grid-rows-3">

        <!-- PAIS -->
        <div class="mb-4">
            <label for="country" class="block text-gray-700 font-bold mb-2">País:</label>
            <div class="relative">
                <select id="country" name="country"
                    class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
                    <option disabled selected value="">Selecciona tu país</option>
                    <option v-for="country of countries.countriesData" :value="country.id">{{ country.name }}</option>
                </select>
                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                    <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                        <path d="M0 0h20v20H0z" fill="none" />
                        <path d="M7 10l5 5 5-5z" />
                    </svg>
                </div>
            </div>
        </div>

        <!-- GENERO -->
        <div class="mb-4">
            <label for="gender" class="block text-gray-700 font-bold mb-2">Género:</label>
            <div>
                <label class="inline-flex items-center">
                    <input type="radio" v-model="gender" name="gender" value="male" class="form-radio h-5 w-5 text-gray-600"
                        checked>
                    <span class="ml-2 text-gray-700">Masculino</span>
                </label>
                <label class="inline-flex items-center ml-6">
                    <input type="radio" v-model="gender" name="gender" value="female"
                        class="form-radio h-5 w-5 text-gray-600">
                    <span class="ml-2 text-gray-700">Femenino</span>
                </label>
            </div>
        </div>

        <!-- PRIMER NOMBRE -->
        <div class="mb-4">
            <label for="first_name" class="block text-gray-700 font-bold mb-2">Primer nombre:</label>
            <div class="relative">
                <input v-model="firstName" type="text" id="first_name" name="first_name" autocomplete="off"
                    placeholder="Ingresa tu primer nombre"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validateFirstName">
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="firstName.length >= 3">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="firstName && firstName.length >= 1">
                    <i class="fas fa-times text-red-500"></i>
                </div>
            </div>
            <div v-if="firstName.length < 3 && firstName.length >= 1" class="text-red-500 text-xs mt-1">
                <span v-if="!firstName">El primer nombre es obligatorio.</span>
                <span v-else-if="firstName.length < 3">El primer nombre debe tener al menos 3 letras.</span>
                <span v-else-if="firstName.length > 70">El primer nombre no puede tener más de 70 letras.</span>
                <span v-else>El primer nombre solo puede contener letras.</span>
            </div>
        </div>

        <!-- SEGUNDO NOMBRE -->
        <div class="mb-4">
            <label for="second_name" class="block text-gray-700 font-bold mb-2">Segundo nombre:</label>
            <div class="relative">
                <input v-model="secondName" type="text" id="second_name" name="second_name" autocomplete="off"
                    placeholder="Ingresa tu segundo nombre"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validateSecondName">
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="secondName.length >= 3">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2"
                    v-else-if="secondName && secondName.length >= 1">
                    <i class="fas fa-times text-red-500"></i>
                </div>
            </div>
            <div v-if="secondName.length < 3 && secondName.length >= 1" class="text-red-500 text-xs mt-1">
                <span v-if="!secondName">El segundo nombre es obligatorio.</span>
                <span v-else-if="secondName.length < 3">El segundo nombre debe tener al menos 3 letras.</span>
                <span v-else-if="secondName.length > 70">El segundo nombre no puede tener más de 70 letras.</span>
                <span v-else>El segundo nombre solo puede contener letras.</span>
            </div>
        </div>

        <!-- FECHA DE NACIMIENTO -->
        <div class="mt-4">
            <label for="birthdate" class="block text-gray-700 font-bold mb-2">Fecha de nacimiento:</label>
            <input v-model="birthdate" type="date" id="birthdate" @change="validateBirthdate"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline">
            <div v-if="birthdateError" class="mt-1 text-xs text-red-500">{{ birthdateError }}</div>
        </div>

        <!-- PAIS -->
        <div class="mb-4">
            <label for="country" class="block text-gray-700 font-bold mb-2">País:</label>
            <div class="relative">
                <select v-model="selectedOption"
                    class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
                    <option disabled value="">Seleccione un tipo de documento</option>
                    <option v-for="option in documentTypeOptions" :value="option.value">{{ option.label }}</option>
                </select>
                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                    <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                        <path d="M0 0h20v20H0z" fill="none" />
                        <path d="M7 10l5 5 5-5z" />
                    </svg>
                </div>
            </div>
        </div>

        <!-- NÚMERO DE DOCUMENTO -->
        <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="numDocumento">
                Número de documento:
            </label>
            <input
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                id="numDocumento" type="text" pattern="[0-9]{5,}" v-model="numDocumento" @input="validateNumDocumento"
                autocomplete="off">
            <p v-if="numDocumentoError" class="text-red-500 text-xs italic">{{ numDocumentoError }}</p>
        </div>

        <!-- FOTO DOCUMENTO - FRENTE -->
        <div class="mb-4">
            <label for="file-input-front" class="block text-gray-700 font-bold mb-2">Foto documento - Frente:</label>
            <input type="file" id="file-input-front" accept=".jpg" @change="handleFileUploadFront"
                class="border-gray-300 focus:border-indigo-500 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
            <p v-if="fileErrorFront" class="text-red-500 text-xs italic">{{ fileErrorFront }}</p>
        </div>

        <!-- FOTO DOCUMENTO - REVERSO -->
        <div class="mb-4">
            <label for="file-input-back" class="block text-gray-700 font-bold mb-2">Foto documento - Reverso:</label>
            <input type="file" id="file-input-back" accept=".jpg" @change="handleFileUploadBack"
                class="border-gray-300 focus:border-indigo-500 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
            <p v-if="fileErrorBack" class="text-red-500 text-xs italic">{{ fileErrorBack }}</p>
        </div>

    </div>
    <!-- Step 1 -->
    <!-- <div v-if="currentStep === 1">
    </div> -->
</template>

<script>

import vSelect from 'vue-select';
import countries from '../../public/data/countries.json'

export default {
    name: 'StepOne',
    components: {
        vSelect,
    },
    data() {
        return {
            selectedCountry: null,
            countries: countries,
            birthdate: null,
            birthdateError: null,
            documentTypeOptions: [
                { value: 'cc', label: 'Cedula de ciudadanía' },
                { value: 'pp', label: 'Pasaporte' },
                { value: 'ce', label: 'Cedula de extranjería' }
            ],
            selectedOption: '',
            numDocumento: null,
            numDocumentoError: null,
            firstName: '',
            secondName: '',
            numDocumento: '',
            numDocumentoError: '',
            fileErrorFront: '',
            fileErrorBack: ''
        };
    },
    methods: {
        validateFirstName() {
            const regex = /^[a-zA-Z]*$/
            if (this.firstName.length > 0 && !regex.test(this.firstName)) {
                this.firstName = this.firstName.slice(0, -1)
            }
        },
        validateSecondName() {
            const regex = /^[a-zA-Z]*$/
            if (this.secondName.length > 0 && !regex.test(this.secondName)) {
                this.secondName = this.secondName.slice(0, -1)
            }
        },
        validateBirthdate() {
            const birthdate = new Date(this.birthdate)
            const eighteenYearsAgo = new Date()
            eighteenYearsAgo.setFullYear(eighteenYearsAgo.getFullYear() - 18)

            if (birthdate > eighteenYearsAgo) {
                this.birthdateError = "Debes tener al menos 18 años."
            } else {
                this.birthdateError = null
            }
        },
        validateNumDocumento() {
            const numDocumentoRegex = /^[0-9]+$/
            if (!numDocumentoRegex.test(this.numDocumento)) {
                this.numDocumento = this.numDocumento.slice(0, -1)
                this.numDocumentoError = 'El número de documento solo puede contener números.'
            } else if (this.numDocumento.length < 5 && this.numDocumento.length > 0) {
                this.numDocumentoError = 'El número de documento debe tener al menos 5 dígitos.'
            } else {
                this.numDocumentoError = ''
            }
        },
        handleFileUploadFront(e) {
            const file = e.target.files[0]
            const allowedExtensions = /(\.jpg)$/i
            if (!allowedExtensions.exec(file.name)) {
                this.fileErrorFront = 'El archivo debe ser de tipo JPG'
            } else {
                this.fileErrorFront = ''
                // Continúa con el procesamiento del archivo
            }
        },
        handleFileUploadBack(e) {
            const file = e.target.files[0]
            const allowedExtensions = /(\.jpg)$/i
            if (!allowedExtensions.exec(file.name)) {
                this.fileErrorBack = 'El archivo debe ser de tipo JPG'
            } else {
                this.fileErrorBack = ''
                // Continúa con el procesamiento del archivo
            }
        }
    }
};
</script>