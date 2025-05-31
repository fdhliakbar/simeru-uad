<template>
  <div>
    <h2 class="text-lg font-bold mb-2">Jadwal Mata Kuliah</h2>
    <form @submit.prevent="handleCari" class="mb-4 flex gap-2 flex-wrap">
      <select v-model="selectedFakultas" class="border px-2 py-1 rounded">
        <option value="">Pilih Fakultas</option>
        <option value="Teknologi Industri">Teknologi Industri</option>
        <!-- Tambahkan fakultas lain jika perlu -->
      </select>
      <select v-model="selectedProdi" class="border px-2 py-1 rounded">
        <option value="">Pilih Prodi</option>
        <option value="Informatika">Informatika</option>
        <!-- Tambahkan prodi lain jika perlu -->
      </select>
      <button type="submit" class="bg-blue-600 text-white px-4 py-1 rounded">
        Cari
      </button>
    </form>

    <div v-if="showTable">
      <table class="min-w-full border">
        <thead>
          <tr>
            <th
              v-for="header in headers"
              :key="header"
              class="border px-2 py-1"
            >
              {{ header }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, idx) in filteredRows" :key="idx">
            <td
              v-for="header in headers"
              :key="header"
              class="border px-2 py-1"
            >
              {{ row[header] }}
            </td>
          </tr>
        </tbody>
      </table>
      <div v-if="filteredRows.length === 0" class="text-gray-500 mt-2">
        Tidak ada data jadwal.
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import Papa from "papaparse";

const headers = ref([]);
const rows = ref([]);
const selectedFakultas = ref("");
const selectedProdi = ref("");
const showTable = ref(false);

const hariList = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat", "Sabtu"];

// Filter hanya baris yang hari-nya ada di hariList
const filteredRows = computed(() => {
  if (!showTable.value) return [];
  // Baris pertama pada CSV kadang header/hari, pastikan filter hanya baris valid
  return rows.value.filter((row) => {
    // Cek apakah kolom pertama (hari) ada di hariList
    const hari = row[Object.keys(row)[0]]?.trim();
    return hariList.includes(hari);
  });
});

function handleCari() {
  // Validasi sederhana
  if (selectedFakultas.value && selectedProdi.value) {
    showTable.value = true;
  } else {
    showTable.value = false;
    alert("Pilih fakultas dan prodi terlebih dahulu.");
  }
}

onMounted(() => {
  fetch("/model/simeru_informatika.csv")
    .then((res) => res.text())
    .then((csv) => {
      Papa.parse(csv, {
        header: true,
        skipEmptyLines: true,
        complete: (result) => {
          headers.value = result.meta.fields;
          rows.value = result.data;
        },
      });
    });
});
</script>
