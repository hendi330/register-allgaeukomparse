<template>
    <div class="row justify-content-center">


        <div class='col-10 impressum'>
            <h1>Impressum</h1>
            <p>Angaben gemäß § 5 TMG</p>
            <p>Max Muster <br>
                Musterweg<br>
                1345 Musterstadt <br>
            </p>
            <p> <strong>Vertreten durch: </strong><br>
                Max Muster<br>
            </p>
            <p><strong>Kontakt:</strong> <br>
                Telefon: 01234-789456<br>
                Fax: 1234-56789<br>
                E-Mail: <a href='mailto:max@muster.de'>max@muster.de</a><br></p>
            <p><strong>Registereintrag: </strong><br>
                Eintragung im Registergericht: Musterstadt<br>
                Registernummer: 12345<br></p>
            <p><strong>Umsatzsteuer-ID: </strong> <br>
                Umsatzsteuer-Identifikationsnummer gemäß §27a Umsatzsteuergesetz: Musterustid.<br><br>
                <strong>Wirtschafts-ID: </strong><br>
                Musterwirtschaftsid<br>
            </p>
            <p><strong>Aufsichtsbehörde:</strong><br>
                Musteraufsicht Musterstadt<br></p>
            <p><strong>Haftungsausschluss: </strong><br><br><strong>Datenschutz</strong><br><br>
                Die Nutzung unserer Webseite ist in der Regel ohne Angabe personenbezogener Daten möglich. Soweit auf
                unseren
                Seiten personenbezogene Daten (beispielsweise Name, Anschrift oder eMail-Adressen) erhoben werden, erfolgt
                dies,
                soweit möglich, stets auf freiwilliger Basis. Diese Daten werden ohne Ihre ausdrückliche Zustimmung nicht an
                Dritte weitergegeben. <br>
                Wir weisen darauf hin, dass die Datenübertragung im Internet (z.B. bei der Kommunikation per E-Mail)
                Sicherheitslücken aufweisen kann. Ein lückenloser Schutz der Daten vor dem Zugriff durch Dritte ist nicht
                möglich. <br>
                Der Nutzung von im Rahmen der Impressumspflicht veröffentlichten Kontaktdaten durch Dritte zur Übersendung
                von
                nicht ausdrücklich angeforderter Werbung und Informationsmaterialien wird hiermit ausdrücklich
                widersprochen.
                Die Betreiber der Seiten behalten sich ausdrücklich rechtliche Schritte im Falle der unverlangten Zusendung
                von
                Werbeinformationen, etwa durch Spam-Mails, vor.<br>
            </p><br>
            Impressum vom <a href="https://www.impressum-generator.de">Impressum Generator</a> der <a
                href="https://www.kanzlei-hasselbach.de/">Kanzlei Hasselbach, Rechtsanwälte für Arbeitsrecht und
                Familienrecht</a>
        </div>
        <div class="col-10">
            <button class="btn btn-primary" @click="backtostart()">Zurürck zum Anfang</button>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { defineEmits, computed } from 'vue';

const emit = defineEmits(['back-to-start']);
function backtostart() {
    emit('back-to-start');
}
</script>