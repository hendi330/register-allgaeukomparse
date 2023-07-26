
<template>
    <div class="location">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Bitte trag hier deine Adressinformationen ein.</p>
                </div>
            </div>
        </div>

        <div class="row justify-content-center">
            <div class="col-12">
                <div class="row mt-20">


                    <div class="col-7">
                        <label for="street" class="form-label">Straße</label>
                        <input type="text" class="form-control" id="street" v-model="street_input" required>
                        <div class="invalid-feedback" id="street-feedback">
                            Bitte geben sie eine Straße an.
                        </div>
                    </div>
                    <div class="col-4">
                        <label for="housenumber" class="form-label">Hausnummer</label>
                        <input type="text" class="form-control" id="housenumber" placeholder="" v-model="housenumber_input" required>
                        <div class="invalid-feedback" id="housenumber-feedback">
                            Bitte geben sie eine Hausnummer an.
                        </div>
                    </div>
                </div>
                <div class="row mt-20 mb-30">
                    <div class="col-7">
                        <label for="city" class="form-label">Stadt</label>
                        <input type="text" class="form-control" id="city" placeholder="" v-model="city_input" required>
                        <div class="invalid-feedback" id="city-feedback">
                            Bitte geben sie eine Stadt an.
                        </div>
                    </div>

                    <div class="col-4">
                        <label for="plz" class="form-label">Postleitzahl</label>
                        <input type="text" class="form-control" id="plz" placeholder="" v-model="zipcode_input" required>
                        <div class="invalid-feedback" id="plz-feedback">
                            Bitte geben sie eine Postleitzahl an.
                        </div>
                    </div>
                </div>


            </div>
        </div>
        <div class="row justify-content-center margin-bottom-5 mt-3">
            <div class="col-10">
                <div class="row mt-20 mb-20">
                    <div class="btn-group">
                        <button @click="back_to_start()" class="btn btn-danger">Zurück zum Anfang</button>

                        <button class="btn btn-primary" type="button" @click="save_data()" :disabled ="!(street_input && housenumber_input && city_input && zipcode_input)">Weiter</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { defineEmits } from 'vue';
const emit = defineEmits(['save-data', 'back-to-start']);
let street_input = ref(null);
let housenumber_input = ref(null);
let city_input = ref(null);
let zipcode_input = ref(null);


function save_data() {
    // let tmp_arr = ref({
    //     "location": {
    //         "street": street_input.value,
    //         "housenumber": housenumber_input.value,
    //         "city": city_input.value,
    //         "zipcode": zipcode_input.value,
            

    //     }
    // });
    let arr = {
        street: street_input.value,
        housenumber: housenumber_input.value,
        city: city_input.value,
        zip: zipcode_input.value,
    }

    emit('save-data', arr);
}
function back_to_start() {
    emit('back-to-start');
}
</script>