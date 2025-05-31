<template>
  <div class="p-6 bg-gray-50 min-h-screen">
    <!-- Watch Now & Slider -->
    <!-- Use splide library for image slider -->
    <div class="bg-white rounded-2xl p-6 shadow mb-6">
      <div class="flex justify-between items-center mb-4">
        <div>
          <div class="text-xl font-bold">Watch Now</div>
          <div class="text-xs text-gray-400">Studying Streams</div>
        </div>
        <button class="text-gray-400 hover:text-blue-500">
          <svg
            class="w-5 h-5"
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
      <!-- Splide Slider -->
      <Splide
        :options="{ perPage: 7, gap: '1rem', pagination: false, arrows: false }"
        class="mb-4"
      >
        <SplideSlide v-for="(img, idx) in sliderImages" :key="idx">
          <img
            :src="img"
            class="rounded-full w-16 h-16 object-cover border-4 border-white shadow transition-transform duration-300 hover:scale-110 hover:ring-4 hover:ring-blue-200"
            alt="User"
          />
        </SplideSlide>
      </Splide>
      <!-- Upcoming -->
      <div class="flex gap-6 mt-2">
        <div
          v-for="(item, idx) in upcoming"
          :key="idx"
          class="flex-1 flex items-center gap-3 bg-gray-50 rounded-xl p-3"
        >
          <img :src="item.icon" class="w-8 h-8" alt="icon" />
          <div>
            <div class="font-semibold text-sm">{{ item.title }}</div>
            <div class="flex items-center gap-2 text-xs text-gray-400">
              <span>{{ item.date }}</span>
              <span :class="item.statusClass">{{ item.status }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- My Classes -->
    <div class="mb-6">
      <div class="flex justify-between items-center mb-3">
        <div class="text-lg font-bold">My Classes</div>
        <button class="text-gray-400 text-xs hover:text-blue-500">
          See All &gt;
        </button>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div
          v-for="(cls, idx) in classes"
          :key="idx"
          class="bg-white rounded-2xl p-6 shadow hover:shadow-lg transition-shadow"
        >
          <div class="flex items-center gap-3 mb-4">
            <img
              :src="cls.icon"
              class="w-12 h-12 rounded-xl"
              alt="class icon"
            />
            <div>
              <div class="font-semibold">{{ cls.title }}</div>
              <div class="text-xs text-gray-400">{{ cls.teacher }}</div>
            </div>
          </div>
          <div class="grid grid-cols-2 gap-3 mb-4">
            <div
              v-for="(info, i) in cls.info"
              :key="i"
              class="flex items-center gap-2"
            >
              <img :src="info.icon" class="w-5 h-5" alt="icon" />
              <span class="text-xs text-gray-600">{{ info.text }}</span>
            </div>
          </div>
          <button
            class="border border-orange-400 text-orange-400 px-4 py-1 rounded-lg font-semibold text-sm hover:bg-orange-50 transition"
          >
            View Class
          </button>
        </div>
      </div>
    </div>

    <!-- Today Tasks -->
    <div>
      <div class="text-lg font-bold mb-2">Today Tasks</div>
      <div class="text-xs text-gray-400 mb-3">6 Result</div>
      <div class="space-y-3">
        <div
          v-for="(task, idx) in tasks"
          :key="idx"
          class="bg-white rounded-xl flex items-center p-3 shadow hover:shadow-md transition group"
        >
          <img
            :src="task.img"
            class="w-14 h-14 rounded-xl object-cover mr-4"
            alt="task"
          />
          <div class="flex-1">
            <div class="font-semibold text-sm">{{ task.title }}</div>
            <div class="text-xs text-gray-400">{{ task.category }}</div>
          </div>
          <div class="text-xs text-gray-400 mr-4">{{ task.date }}</div>
          <div>
            <span
              :class="[
                'inline-block w-6 h-6 rounded-full flex items-center justify-center',
                task.done
                  ? 'bg-green-100 text-green-500'
                  : 'bg-red-100 text-red-500',
              ]"
            >
              <svg
                v-if="task.done"
                class="w-4 h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M5 13l4 4L19 7"
                />
              </svg>
              <svg
                v-else
                class="w-4 h-4"
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
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import "@splidejs/vue-splide/css";
import { Splide, SplideSlide } from "@splidejs/vue-splide";

// Dummy images and icons (replace with your assets)
const sliderImages = [
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
  "/assets/images/icons/person_icon.jpg",
];

const upcoming = [
  {
    icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/powerpoint/powerpoint-original.svg",
    title: "Presentation for Branding",
    date: "13/09",
    status: "Due Soon",
    statusClass: "text-orange-400 font-semibold",
  },
  {
    icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/word/word-original.svg",
    title: "Task Document for HCI",
    date: "13/09",
    status: "Due Soon",
    statusClass: "text-orange-400 font-semibold",
  },
  {
    icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/excel/excel-original.svg",
    title: "Data for UI/UX Research",
    date: "13/09",
    status: "Soon",
    statusClass: "text-green-500 font-semibold",
  },
];

const classes = [
  {
    icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg",
    title: "Interaction Engineering",
    teacher: "Jhon Smith",
    info: [
      {
        icon: "https://img.icons8.com/color/48/000000/classroom.png",
        text: "B Class",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/stack-of-books.png",
        text: "3 Credit",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/conference-call.png",
        text: "30 Student",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/clock--v1.png",
        text: "3 Hours/Week",
      },
    ],
  },
  {
    icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/photoshop/photoshop-plain.svg",
    title: "3D Art Learning",
    teacher: "Alex Jene",
    info: [
      {
        icon: "https://img.icons8.com/color/48/000000/classroom.png",
        text: "C Class",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/stack-of-books.png",
        text: "7 Credit",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/conference-call.png",
        text: "35 Student",
      },
      {
        icon: "https://img.icons8.com/color/48/000000/clock--v1.png",
        text: "5 Hours/Week",
      },
    ],
  },
];

const tasks = [
  {
    img: "https://images.unsplash.com/photo-1519389950473-47ba0277781c?auto=format&fit=facearea&w=256&q=80",
    title: "Task Document for HCI",
    category: "UI/UX Design",
    date: "February, 28",
    done: true,
  },
  {
    img: "https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=facearea&w=256&q=80",
    title: "Task Analysis for IA",
    category: "Information Architecture",
    date: "March, 1",
    done: false,
  },
];
</script>

<style scoped>
/* Custom hover for slider images */
.splide__slide img {
  transition: transform 0.3s, box-shadow 0.3s;
}
.splide__slide img:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 20px 0 rgba(59, 130, 246, 0.15);
}
</style>
