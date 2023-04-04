<template>
    <div class="grid gap-4 grid-cols-3 grid-rows-3">
        <!-- CORREO ELECTÓNICO -->
        <div class="mb-4">
            <label for="email" class="block text-gray-700 font-bold mb-2">Correo electrónico:</label>
            <div class="relative">
                <input v-model="email" type="email" id="email" name="email" autocomplete="off"
                    placeholder="Ingresa tu correo electrónico"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validateEmail">
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="isEmailValid">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="email">
                    <i class="fas fa-times text-red-500"></i>
                </div>
            </div>
            <div v-if="!isEmailValid && email" class="text-red-500 text-xs mt-1">
                <span>Por favor, introduce un correo electrónico válido.</span>
            </div>
        </div>

        <!-- CONTRASEÑA -->
        <div class="mb-6">
            <label for="password" class="block text-gray-700 font-bold mb-2">Contraseña:</label>
            <div class="relative">
                <input v-model="password" type="password" id="password" name="password" autocomplete="off"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validatePassword" />
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="password.length >= 6">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="password && password.length >= 1">
                    <i class="fas fa-times text-red-500"></i>
                </div>
                <!-- <span class="ml-2">{‌{ passwordIcon }}</span> -->
                <div v-if="!isPasswordValid && password" class="text-red-500 text-xs mt-1">
                    <span>La contraseña debe tener mas de 6 caracteres.</span>
                </div>
            </div>
        </div>





        <!-- CONFIRMACIÓN DE CONTRASEÑA -->
        <div class="mb-6">
            <label for="confirmPassword" class="block text-gray-700 font-bold mb-2">Confirmar contraseña:</label>
            <div class="relative">
                <input v-model="confirmPassword" type="password" id="confirmPassword" name="confirmPassword" autocomplete="off"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validateConfirmPassword" />
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="password === confirmPassword && password.length >= 1">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="!password === confirmPassword">
                    <i class="fas fa-times text-red-500"></i>
                </div>
                <div v-if="!password === confirmPassword && password.length >= 1" class="text-red-500 text-xs mt-1">
                    <span>Las contraseñas no coinciden.</span>
                </div>
            </div>
        </div>


        <!-- TELEFONO -->
        <div class="mb-6">
            <label for="phone" class="block text-gray-700 font-bold mb-2">Teléfono:</label>
            <input v-model="phone" type="tel" id="phone" name="phone" autocomplete="off"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                @input="validatePhone" />
        </div>

        <!-- MOBILE -->
        <div class="mb-6">
            <label for="mobile" class="block text-gray-700 font-bold mb-2">Celular:</label>
            <input v-model="mobile" type="tel" id="mobile" name="mobile" autocomplete="off"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                @input="validateMobile" />
        </div>
    </div>
</template>

<script>
export default {
    name: 'StepTwo',
    data() {
        return {
            email: '',
            isEmailValid: false,
            password: '',
            isPasswordValid: false,
            confirmPassword: '',
            phoneNumber: '',
            mobileNumber: '',
            formIsValid: false,
        }
    },
    computed: {
        isEmailValid() {
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;
            return emailRegex.test(this.email);
        },
        isPasswordValid() {
            return this.password.length >= 6;
        },
        isConfirmPasswordValid() {
            return this.password === this.confirmPassword;
        },
        isPhoneNumberValid() {
            const phoneRegex = /^\d{10}$/;
            return phoneRegex.test(this.phoneNumber);
        },
        isMobileNumberValid() {
            const mobileRegex = /^\d{10}$/;
            return mobileRegex.test(this.mobileNumber);
        },
    },
    watch: {
        isEmailValid() {
            this.checkFormValidity();
        },
        isPasswordValid() {
            this.checkFormValidity();
        },
        isConfirmPasswordValid() {
            this.checkFormValidity();
        },
        isPhoneNumberValid() {
            this.checkFormValidity();
        },
        isMobileNumberValid() {
            this.checkFormValidity();
        },
    },
    methods: {
        checkFormValidity() {
            this.formIsValid =
                this.isEmailValid &&
                this.isPasswordValid &&
                this.isConfirmPasswordValid &&
                this.isPhoneNumberValid &&
                this.isMobileNumberValid;
        },
        validateEmail() {
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            this.isEmailValid = emailRegex.test(this.email);
        },
        validatePassword() {

        }
    },
}
</script>