<template>
  <aside
    :class="[
      'fixed top-0 right-0 h-full bg-white shadow-lg z-30 transition-transform duration-200',
      openSidebar ? 'translate-x-0' : 'translate-x-full',
      'w-80 max-w-full',
    ]"
  >
    <div class="flex flex-col items-center py-8 px-4 h-full">
      <!-- Icon menu atas -->
      <div class="flex justify-end w-full gap-4 mb-6">
        <button class="text-gray-400 hover:text-blue-500">
          <svg
            class="h-6 w-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
        </button>
        <button class="text-gray-400 hover:text-blue-500">
          <svg
            class="h-6 w-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M17 8h2a2 2 0 012 2v10a2 2 0 01-2 2H5a2 2 0 01-2-2V10a2 2 0 012-2h2"
            />
          </svg>
        </button>
        <button class="text-gray-400 hover:text-blue-500">
          <svg
            class="h-6 w-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M21 15a2 2 0 01-2 2H5a2 2 0 01-2-2V7a2 2 0 012-2h14a2 2 0 012 2v8z"
            />
          </svg>
        </button>
        <button class="text-orange-400 hover:text-orange-600">
          <svg
            class="h-6 w-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M17 16l4-4m0 0l-4-4m4 4H7"
            />
          </svg>
        </button>
      </div>
      <!-- Foto profil -->
      <div class="relative mb-4">
        <img
          :src="profileImg"
          alt="Profile"
          class="rounded-xl w-24 h-24 object-cover border-4 border-white shadow"
        />
        <div
          class="absolute -top-2 -right-2 w-8 h-8 bg-yellow-400 rounded-lg"
        ></div>
      </div>
      <!-- Nama dan role -->
      <div class="text-center mb-2">
        <div class="text-xl font-semibold">Kiril Poliakov</div>
        <div
          class="inline-block bg-orange-100 text-orange-500 px-3 py-1 rounded mt-1 text-xs font-semibold"
        >
          SOFTWARE ENGINEER
        </div>
      </div>
      <!-- Kalender -->
      <div class="w-full mt-8">
        <div class="flex justify-between items-center mb-2">
          <button @click="prevMonth" class="text-gray-400 hover:text-blue-500">
            <svg
              class="h-5 w-5"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 19l-7-7 7-7"
              />
            </svg>
          </button>
          <div class="font-semibold">{{ monthYear }}</div>
          <button @click="nextMonth" class="text-gray-400 hover:text-blue-500">
            <svg
              class="h-5 w-5"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              />
            </svg>
          </button>
        </div>
        <div class="grid grid-cols-7 text-center text-xs text-gray-400 mb-1">
          <div v-for="d in days" :key="d">{{ d }}</div>
        </div>
        <div class="grid grid-cols-7 text-center">
          <template v-for="(blank, i) in blanks" :key="'b' + i">
            <div></div>
          </template>
          <template v-for="day in daysInMonth" :key="day">
            <div
              class="py-1 my-0.5 rounded-full cursor-pointer"
              :class="{
                'bg-blue-600 text-white font-bold': isToday(day),
                'text-gray-700 hover:bg-blue-100': !isToday(day),
              }"
            >
              {{ day }}
            </div>
          </template>
        </div>
      </div>
    </div>
    <!-- Hamburger untuk mobile -->
    <button
      class="fixed top-4 right-4 z-40 md:hidden bg-white p-2 rounded shadow"
      @click="openSidebar = !openSidebar"
    >
      <svg
        v-if="!openSidebar"
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"
        />
      </svg>
      <svg
        v-else
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M6 18L18 6M6 6l12 12"
        />
      </svg>
    </button>
    <!-- Overlay mobile -->
    <div
      v-if="openSidebar"
      class="fixed inset-0 bg-black bg-opacity-30 z-20 md:hidden"
      @click="openSidebar = false"
    ></div>
  </aside>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from "vue";
// Use a placeholder image if the local asset does not exist
import profileImg from "@/assets/images/icons/dj.png";

const openSidebar = ref(
  typeof window !== "undefined" ? window.innerWidth >= 768 : false
);

function handleResize() {
  if (typeof window !== "undefined") {
    openSidebar.value = window.innerWidth >= 768;
  }
}
onMounted(() => {
  window.addEventListener("resize", handleResize);
});
onBeforeUnmount(() => {
  window.removeEventListener("resize", handleResize);
});

// Kalender logic
const today = new Date();
const currentMonth = ref(today.getMonth());
const currentYear = ref(today.getFullYear());

const days = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];

const monthYear = computed(() => {
  return (
    today.toLocaleString("default", { month: "long" }) + " " + currentYear.value
  );
});

const daysInMonth = computed(() => {
  const date = new Date(currentYear.value, currentMonth.value + 1, 0);
  return Array.from({ length: date.getDate() }, (_, i) => i + 1);
});

const blanks = computed(() => {
  const firstDay = new Date(currentYear.value, currentMonth.value, 1).getDay();
  return Array.from({ length: firstDay });
});

function isToday(day) {
  return (
    day === today.getDate() &&
    currentMonth.value === today.getMonth() &&
    currentYear.value === today.getFullYear()
  );
}

function prevMonth() {
  if (currentMonth.value === 0) {
    currentMonth.value = 11;
    currentYear.value -= 1;
  } else {
    currentMonth.value -= 1;
  }
}
function nextMonth() {
  if (currentMonth.value === 11) {
    currentMonth.value = 0;
    currentYear.value += 1;
  } else {
    currentMonth.value += 1;
  }
}
</script>

<style scoped>
aside {
  min-width: 320px;
  max-width: 100vw;
}
@media (max-width: 767px) {
  aside {
    width: 100vw !important;
    min-width: 0 !important;
    right: 0;
  }
}
</style>
