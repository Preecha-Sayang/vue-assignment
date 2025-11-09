<template>
  <div class="course-card">
    <h3>ชื่อคอร์ส: {{ props.course.title }}</h3>
    <p>ราคา: {{ props.course.price }} บาท</p>
    <button @click="toggleFavorite">
      {{ isFavorite ? "💔 เอาออกจากรายการโปรด" : "❤️ เพิ่มในรายการโปรด" }}
    </button>
  </div>
</template>

<script setup>
import { useFavoriteStore } from "../stores/favorite";
import { computed } from "vue";

// รับ prop
const props = defineProps({
  course: Object
});

// ใช้ store
const store = useFavoriteStore();

// ใช้ computed เพื่อตรวจสอบ favorite (reactive)
const isFavorite = computed(() => store.favorites.includes(props.course.title));

// ฟังก์ชันเพิ่ม/เอาออก favorites
function toggleFavorite() {
  if (isFavorite.value) {
    store.favorites = store.favorites.filter(c => c !== props.course.title);
  } else {
    store.addFavorite(props.course.title);
  }
}
</script>



<style scoped>
.course-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
  max-width: 600px;
  margin: auto;
  padding: 16px;
}

.course-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fafafa;
  padding: 12px 16px;
}

h3 {
  margin: 0;
  font-size: 16px;
  font-weight: 600;
}

p {
  margin: 0;
  color: #555;
}

button {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background-color: #2c9c6d;
}
</style>
