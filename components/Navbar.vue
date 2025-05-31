<template>
  <nav>
    <!-- Sidebar -->
    <div
      :class="[
        'fixed top-0 left-0 h-full bg-white shadow-lg z-30 transition-transform duration-200',
        openSidebar ? 'translate-x-0' : '-translate-x-full',
        'w-64',
      ]"
      style="min-width: 220px"
    >
      <div class="flex flex-col h-full">
        <!-- Logo -->
        <div class="flex items-center gap-2 px-6 py-6">
          <!-- Ganti src sesuai logo -->
          <img
            src="/assets/images/icons/3d-piggy-bank.png"
            alt="Logo"
            class="h-8 w-8"
          />
          <span class="text-xl font-bold text-blue-600">SIMERU</span>
        </div>
        <!-- Menu -->
        <ul class="flex-1 px-4 space-y-2">
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-gray-700"
            >
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
                  d="M3 12l2-2m0 0l7-7 7 7M13 5v6h6"
                ></path>
              </svg>
              <span>Overview</span>
            </a>
          </li>
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-blue-600 font-semibold"
            >
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
                  d="M9 17v-6a2 2 0 012-2h2a2 2 0 012 2v6"
                ></path>
              </svg>
              <span>Courses</span>
            </a>
          </li>
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-gray-700"
            >
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
                  d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                ></path>
              </svg>
              <span>Schedule</span>
            </a>
          </li>
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-gray-700"
            >
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
                  d="M17 8h2a2 2 0 012 2v10a2 2 0 01-2 2H5a2 2 0 01-2-2V10a2 2 0 012-2h2"
                ></path>
              </svg>
              <span>Chat</span>
            </a>
          </li>
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-gray-700"
            >
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
                  d="M12 4v16m8-8H4"
                ></path>
              </svg>
              <span>Calender</span>
            </a>
          </li>
          <li>
            <a
              href="#"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-blue-50 text-gray-700"
            >
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
                  d="M12 4v16m8-8H4"
                ></path>
              </svg>
              <span>Setting</span>
            </a>
          </li>
        </ul>
        <!-- Product update box -->
        <div class="p-4 mt-auto">
          <div class="bg-blue-50 rounded-xl p-4 flex flex-col items-center">
            <img
              src="/assets/images/icons/3d-piggy-bank.png"
              alt="Update"
              class="h-16 mb-2"
            />
            <div class="text-sm font-semibold text-blue-700 mb-1">
              Get product update
            </div>
            <input
              type="email"
              placeholder="Enter your email here"
              class="w-full px-2 py-1 rounded border text-xs"
            />
          </div>
        </div>
      </div>
    </div>
    <!-- Hamburger Button -->
    <button
      class="fixed top-4 left-4 z-40 md:hidden bg-white p-2 rounded shadow"
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
    <!-- Overlay for mobile -->
    <div
      v-if="openSidebar"
      class="fixed inset-0 bg-black bg-opacity-30 z-20 md:hidden"
      @click="openSidebar = false"
    ></div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
const openSidebar = ref(true);

function handleResize() {
  openSidebar.value = window.innerWidth >= 768;
}

onMounted(() => {
  handleResize(); // set nilai awal setelah mounted
  window.addEventListener("resize", handleResize);
});
onBeforeUnmount(() => {
  window.removeEventListener("resize", handleResize);
});
</script>

<style scoped>
@media (min-width: 768px) {
  nav > div {
    transform: translateX(0) !important;
    position: static !important;
  }
  .fixed.top-4.left-4 {
    display: none !important;
  }
}
body {
  padding-left: 0;
}
@media (min-width: 768px) {
  body {
    padding-left: 16rem; /* width sidebar */
  }
}
</style>
