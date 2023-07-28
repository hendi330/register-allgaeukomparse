

<template>
  <div class="container centerdiv">
    <main>
      <div v-if="!readmebool">
        <confirmations @read-me="read_me" @all-confirmed="incrementCurrentForm"
          v-if="check_active_form('confirmation')" />

        <komparseform v-else-if="check_active_form('komparse')" @back-to-start="reset_active_job()"
          @save-data="add_data_to_array" />
        <personalInfo v-else-if="check_active_form('personalinfo')" @back-to-start="reset_active_job()"
          @save-data="add_data_to_array" />
        <location v-else-if="check_active_form('location')" @back-to-start="reset_active_job()"
          @save-data="registration_complete" />
      </div>
      <!--<personalInfo v-if="forms[current_form]" main_heading="Registrieren" sub_heading ="Um dich zu registrieren musst du alle felder ausfüllen."/> -->
      <div id="readme" v-else-if="readmebool">
        <datenschutzform @back-to-start="dont_read_me" v-if="agb" />
        <impressumform @back-to-start="dont_read_me" v-else />
      </div>


    </main>
  </div>
</template>
<script setup>

import personalInfo from './components/personalinfo.vue'
import location from './components/location.vue'
import confirmations from './components/confirmations.vue'
import komparseform from './components/komparse.vue'
import datenschutzform from './components/datenschutz.vue'
import impressumform from './components/impressum.vue'
//wie viele forms, welche forms. 
import { ref, toRaw, unref, onMounted } from 'vue';
let registration_infos = ref([]);

let current_form = ref(0);
let readmebool = ref(false);
let agb = ref(false);
console.log(current_form);
let hash = ref("");
console.log("hash");
console.log(hash);
console.log(hash.value);
let active_job = ref("confirmation");

onMounted(() => {
  console.log("mounted");
  hash.value = check_url_for_hash();
  console.log(hash.value);
  check_hash(hash.value);

});
let forms = ref({
  "confirmation": { "active": true, "order": 0 },
  "komparse": { "active": true, "order": 1 },
  "personalinfo": { "active": true, "order": 2 },
  "location": { "active": true, "order": 3 },
});


function check_url_for_hash() {
  //get hash from url, which is everything after .de/
  let hashtmp = window.location.href;
  console.log(hashtmp);
  //get hash from url, which is everything after .de/
  // hashtmp = hashtmp.split(".de/")[1];
  hashtmp = hashtmp.split("5173/")[1];
  console.log(hashtmp);
  return hashtmp;

  //check if the hash is valid, with fetch(api... /hash/valid)
}
async function check_hash(hash_val) {

  fetch("https://api.allgaeu-komparsen.de/hash/valid", {
  // fetch("http://localhost:5174/hash/valid", {
    method: "POST",
    body: JSON.stringify(hash_val),
    headers: {
      "Content-Type": "application/json"
    }
  })
    .then(response => response.json())
    .then(data => {
      console.log("returned data", data);
      if (data) {
        //if hash is valid, show the forms
        console.log("hash is valid");
        return true;
      }
      else {
        //if hash is not valid, show error message
        console.log("hash is not valid");
        return false;
      }
    })

  // console.log(data);
  // return data;
}


function dont_read_me() {
  readmebool.value = false;
}
function read_me(type) {
  readmebool.value = true;
  if (type == "agb") {
    agb.value = true;
  }
  else {
    agb.value = false;
  }
}

function reset_active_job() {
  active_job.value = "confirmation";
  current_form.value = 0;
  forms.value["confirmation"].active = true;
  forms.value["komparse"].active = false;
  forms.value["personalinfo"].active = true;
  forms.value["location"].active = true;
}
const incrementCurrentForm = () => {
  //immer wenn  eine neue form angezeigt werden soll
  current_form.value = (current_form.value + 1);
  forms.value[active_job.value].active = !forms.value[active_job.value].active

};
function start_registration() {
  incrementCurrentForm();
  // let tmp_arr = [];
  // tmp_arr.push({ "cook": forms.value.cook.active });
  // tmp_arr.push({ "komparse": forms.value.komparse.active });
  // tmp_arr.push({ "umsetzer": forms.value.umsetzer.active });
  // tmp_arr.push({ "service": forms.value.service.active });
  // console.log(registration_infos);
  // // registration_infos.value.push(tmp_arr.value);
  // console.log(registration_infos);

}
console.log(forms.value["komparse"]);
function check_active_form(job) {
  //check first if form is even active
  if (forms.value[job].active) {
    /*if form is active check if currentform equals the index (order)
    if (forms.value[job].order == current_form.value) {

      console.log("return true");
      return true;
    }*/
    active_job.value = job;
    return true;


  }
  //if not 
  else {
    return false;
  }
}


function add_data_to_array(data) {
  registration_infos.value.push(data);
  console.log(registration_infos);
  incrementCurrentForm();
}

function registration_complete(data) {
  registration_infos.value.push(data);
  console.log(registration_infos);
  // retrieve information from proxy object
  let reg = toRaw(registration_infos.value);

  // merge the properties from all registration_info objects into one
  let fullobj = {};
  reg.forEach(element => {
    // do encodeURIComponent() for every element in the object
    Object.keys(element).forEach(key => {
      element[key] = encodeURIComponent(element[key]);
    });
    fullobj = { ...fullobj, ...element };
  });

  console.log("fullobj", fullobj);
  send_data(fullobj);
}

function send_data(obj) {
  // for files, convert them to base64 images and send them inside the body, seperate multiple files with linebreaks
  // make sure to escape equal signs following the base64 string with %3D
  let body = "";

  console.log(obj);
  // files.forEach(file => {
  //   let key = "umsetzer_driversLincense_back"
  //   let filename = "red dot.png";
  //   let type = "image/png";
  //   let base64content = "iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVQI12P4//8/w38GIAXDIBKE0DHxgljNBAAO9TXL0Y4OHwAAAABJRU5ErkJggg=="

  //   body += `key=${encodeURIComponent(key)}&filename=${encodeURIComponent(filename)}&content=data:${encodeURIComponent(type)};base64, ${encodeURIComponent(base64content)}\n`;
  // })


  let data = new FormData();
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      data.append(key, obj[key]);
    }
  }


  if (obj.komparse_pic1) {
    data.set("picture1", obj.picture1);
  }
  if (obj.komparse_pic2) {
    data.set("picture2", obj.picture2);
  }


  console.log(body);
  if (check_hash(hash.value)) {
    // fetch("http://localhost:5174/users/add", {
      fetch("https://api.allgaeu-komparsen.de/users/add", {
      method: "POST",
      body: data,
      // headers: obj,
    })
      .then(response => response.json())
      .then(data => {
        console.log("returned data", data);
        fetch("https://api.allgaeu-komparsen.de/hash/delete", {
        // fetch("http://localhost:5174/hash/delete", {
          method: "POST",
          body: JSON.stringify(hash.value),
          headers: {
            "Content-Type": "application/json"
          }
        })

      })
      .catch(error => {
        console.error(error);
      });
  }
}


</script>
<!--
<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
-->