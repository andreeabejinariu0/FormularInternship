<script setup>
import { ref } from "vue";
import { onMounted } from "vue";
import axios from "axios";

const nume = ref("");
const prenume = ref("");
const dataDeNastere = ref("");
const comentariu = ref("");

onMounted(() => {
  console.log("Component mounted.");
});

async function formSubmit() {

  let currentObj = this;

  axios
    .post("http://laravel.test/forms", {
      nume: nume.value,
      prenume: prenume.value,
      data: dataDeNastere.value,
      comentariu: comentariu.value,
    })
    .then(function (response) {
      currentObj.output = response.data;
    })
    .catch(function (error) {
      console.log(error);
      currentObj.output = error;
    });

    console.log("in functia de trimitere");
}
</script>

<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-md-8 mt-3">
        <div class="card">
          <div class="card-header" style="background-color: #b7339d; color: #fff;">Formular</div>

          <div class="card-body">
            <div>
              <strong>Nume:</strong>
              <input type="text" class="form-control" v-model="nume" style="background-color: #f2f2f2;" />
              <br>
              <strong>Prenume:</strong>
              <input type="text" class="form-control" v-model="prenume" style="background-color: #f2f2f2;" />
              <br>
              <strong>Data de naștere:</strong>
              <input type="date" class="form-control" v-model="dataDeNastere" style="background-color: #f2f2f2;" />
              <br>
              <strong>Comentariu:</strong>
              <input type="text" class="form-control" v-model="comentariu" style="background-color: #f2f2f2;" />
              <br>

              <button class="btn btn-success" @click="formSubmit()" style="background-color: #b7339d; color: #fff;">Trimite</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



