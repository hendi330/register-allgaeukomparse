<template>
    <div class="confirmations_class">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Das ist das Anmeldeformular für Streetkitchen. Wir sind ein
                        Unternehmen, dass sich aufs Catering spezialisiert hat und wir suchen noch Helfer!</p>
                    <p class="lead" id="description-for-header">Dafür solltest du mindestens 18 Jahre alt sein und am besten
                        einen Führerschein haben.</p>
                    <p class="lead" id="description-for-header">Außerdem bieten wir die Möglichkeit zur Weiterbildung durch
                        Schulungen.</p>

                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-sm-12 col-md-10 col-lg-9">
                <div class="pricing-header px-3 py-3 pb-md-4 mx-auto ">
                    <h1 class="display-4 text-center" id="description-header">Datenschutz</h1>
                    <p class="lead" id="description-for-header">Wir speichern Ihre Daten bei uns in der Datenbank ab, wenn
                        sie
                        damit einverstanden sind klicken sie bitte das Kästchen an.</p>
                    <div class="form-check checkbox_required" id="datenschutz">

                        <input class="form-check-input text-center" type="checkbox" value="" id="datenschutz_checkbox"
                            v-model="isChecked_datenschutz">

                        <label class="form-check-label text-center" for="flexCheckDefault">
                            Ich bin damit einverstanden, dass meine Daten auf dieser Webseite gespeichert werden. Um die
                            Daten
                            zu löschen nehmen Sie kontakt zu uns auf.
                        </label>
                    </div>
                    <p class="lead mt-4" id="description-for-header">Sie können hier unsere <a @click="readMe('agb')"
                            class="link">Datenschutzrichtlinien</a> und <a class="link" @click="readMe('impressum')" >Impressum</a>
                        einsehen.</p>
                    <div class="form-check checkbox_required" id="agbs">

                        <input class="form-check-input" type="checkbox" value="" id="agb_checkbox" v-model="isChecked_agb">

                        <label class="form-check-label text-center" for="flexCheckDefault">
                            Ich habe die AGBs und Datenschutzrichtlinien gelesen und bin mit diesen einverstanden.
                        </label>
                    </div>
                    <p class="lead mt-4" id="description-for-header">Für die Arbeiten ist ein Mindestalter von 18 Jahren
                        benötigt.</p>
                    <div class="form-check checkbox_required" id="alter">

                        <input class="form-check-input" type="checkbox" value="" id="alter_checkbox"
                            v-model="isChecked_alter">

                        <label class="form-check-label text-center" for="flexCheckDefault">
                            Ich bestätige hiermit, dass ich mindestens 18 Jahre alt bin.
                        </label>
                    </div>
                </div>

            </div>
        </div>


        <div class="col-10">
            <div class="row margin-start-10 margin-bottom-5">
                <button type="button" id="confirm_btn" @click="all_confirmed"
                    :class="['btn', 'btn-lg', 'btn-block', 'btn-outline-primary', { disabled: !allChecked }]">Weiter</button>

                <div id="confirmation_feedback" class="invalid-feedback">
                    Bitte wähle mindestens eines der vier verschiedenen Angebote aus.
                </div>
            </div>
        </div>
    </div>
</template> 
<!-- <script>

export default {
    data() {
        return {
            isChecked_datenschutz: false,
            isChecked_agb: false,
            isChecked_alter: false,
        };
    },
   
    computed: {
        allChecked() {
            return this.isChecked_datenschutz && this.isChecked_agb && this.isChecked_alter;
        }
    }
}
</script> -->

<script setup>
import { ref, computed } from 'vue';
import { defineEmits } from 'vue';
let isChecked_datenschutz = ref(false);
let isChecked_agb = ref(false);
let isChecked_alter = ref(false);
const emit = defineEmits(['all-confirmed', 'read-me']);

function all_confirmed() {
    emit('all-confirmed');
}
function readMe(type) {
    emit('read-me', type);
}

//computed wird ausgeführt, wenn eine der drei variablen sich ändern.
//wenn all allchecked false ist, dann wird dem button die klasse disabled hinzugefügt
//wenn alle drei true sind, dann wird disabled entfernt
let allChecked = computed(() =>
    isChecked_datenschutz.value && isChecked_agb.value && isChecked_alter.value
);

</script>