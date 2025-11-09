<template>
  <div class="page-container">
    <header>
      <h2>📚 Course List</h2>
      <!-- ✅ แสดงจำนวนคอร์สที่ถูกใจจาก store -->
      <p>❤️ ถูกใจแล้ว {{ store.favorites.length }} คอร์ส</p>
    </header>

    <div class="form-section">
      <label>ชื่อผู้ใช้:</label>
      <!-- ✅ ผูก v-model กับ store.username -->
      <input v-model="store.username" placeholder="กรอกชื่อของคุณ" />
    </div>

    <div class="course-list">
      <!-- ✅ Render CourseCard -->
<CourseCard
  v-for="course in courses"
  :key="course.id"
  :course="course"
/>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios"; // ✅ import axios
import { useFavoriteStore } from "../stores/favorite"; // ✅ import store
import CourseCard from "../components/CourseCard.vue";

const store = useFavoriteStore(); // ✅ ใช้ store
const courses = ref([]);

// ✅ ดึงข้อมูลจาก API
onMounted(async () => {
  const res = await axios.get("https://fakestoreapi.com/products");
  courses.value = res.data;
});

// ✅ ฟังก์ชันเพิ่ม/เอาออกจาก favorites
function toggleFavorite(courseTitle) {
  if (store.favorites.includes(courseTitle)) {
    store.favorites = store.favorites.filter((c) => c !== courseTitle);
  } else {
    store.addFavorite(courseTitle);
  }
}
</script>

<style scoped>
.page-container {
  max-width: 600px;
  margin: auto;
  text-align: center;
}
.course-list {
  margin-top: 24px;
}
</style>
