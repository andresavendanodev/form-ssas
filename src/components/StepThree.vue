<template>
    <div class="grid gap-4 grid-cols-3 grid-rows-3">

        <!-- DIRECCIÓN DE RESIDENCIA: -->
        <div class="mb-4">
            <label for="address" class="block text-gray-700 font-bold mb-2">Dirección:</label>
            <div class="relative">
                <input v-model="address" type="text" id="address" name="address" autocomplete="off"
                    placeholder="Ingresa tu dirección de residencia"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validateaddress">
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="address.length >= 3">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="address && address.length >= 1">
                    <i class="fas fa-times text-red-500"></i>
                </div>
            </div>
            <div v-if="address.length < 3 && address.length >= 1" class="text-red-500 text-xs mt-1">
                <span v-if="address">la dirección es obligatorio.</span>
            </div>
        </div>

        <!-- CÓDIGO POSTAL -->
        <div class="mb-4">
            <label for="postalCode" class="block text-gray-700 font-bold mb-2">Código postal:</label>
            <div class="relative">
                <input v-model="postalCode" type="text" id="postalCode" name="postalCode" autocomplete="off"
                    placeholder="Ingresa el código postal"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-400 leading-tight focus:outline-none focus:shadow-outline"
                    @input="validatePostalCode">
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-if="postalCode.length >= 3">
                    <i class="fas fa-check text-green-500"></i>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center px-2" v-else-if="postalCode && postalCode.length >= 1">
                    <i class="fas fa-times text-red-500"></i>
                </div>
            </div>
            <div v-if="postalCode.length < 3 && postalCode.length >= 1" class="text-red-500 text-xs mt-1">
                <span v-if="postalCode">El código postal es obligatorio.</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'StepThree',
    data() {
        return {
            address: '',
            postalCode: '',
            isAddressValid: false,
            isPostalCodeValid: false,
        };
    },
    methods: {
        validateAddress() {
            if (this.address.trim() === '') {
                this.isAddressValid = false;
            } else {
                this.isAddressValid = true;
            }
        },
        validatePostalCode() {
            if (this.postalCode.trim() === '') {
                this.isPostalCodeValid = false;
            } else {
                this.isPostalCodeValid = true;
            }
        },
        validateStepThree() {
            if (this.isAddressValid && this.isPostalCodeValid) {
                return true;
            } else {
                return false;
            }
        },
    },
};
</script>

<style scoped></style>