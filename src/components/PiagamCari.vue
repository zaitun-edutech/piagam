<template>
  <section class="mt-5 mb-5" id="pengumuman">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-8">
          <form action="" @submit.prevent="">
            <input
              type="text"
              v-model="cari"
              placeholder="masukkan code piagamnya"
              class="form-control"
              @focus="takTerlihat"
            />
            <button class="btn btn-danger mt-3 mb-5" @click="terlihat">
              Cari
            </button>
          </form>

          <span v-if="show == true" class="mt-5">
            <div v-for="k in cariData" :key="k">
              <div class="card shadow rounded bg-warning" style="width: 18rem">
                <div class="card-body">
                  <p>{{ k.code }}</p>
                  <h5 class="card-title">{{ k.nama }}</h5>
                  <p class="card-text">Status</p>
                  <a :href="k.url" class="btn btn-primary">Dowload</a>
                </div>
              </div>
            </div>
          </span>

          <span v-if="hidden == true">
            <h4 class="text-danger">Data Tidak di Temukan</h4>
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed, reactive, ref } from "vue";
import db from "../db";
const cari = ref("");
const data = reactive(db);
const show = ref(false);
const hidden = ref(false);

const cariData = computed(() => {
  return data.filter((item) => {
    if (cari.value == item.code) {
      return item.code.toLowerCase().includes(cari.value.toLowerCase());
    } else {
      hidden.value == true;
    }
  });
});
const terlihat = () => {
  if (cari.value.length > 0 && cariData.value.length == 1) {
    show.value = true;
    hidden.value = false;
  } else {
    hidden.value = true;
  }
};
const takTerlihat = () => {
  show.value = false;
  hidden.value = false;
};
</script>

<style scoop>
</style>
