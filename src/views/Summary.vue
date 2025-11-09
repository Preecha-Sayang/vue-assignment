<template>
  <div class="page-container">
    <h2>📋 Summary</h2>
    <!-- ✅ ดึงข้อมูลจาก store -->
    <p>ชื่อผู้ใช้: {{ store.username || 'ยังไม่ได้กรอกชื่อ' }}</p>
    <p>จำนวนคอร์สที่ถูกใจ: {{ store.favorites.length }}</p>

    <!-- ✅ เพิ่มรายการคอร์สที่ชอบ (ถ้ามี) -->
    <ul v-if="store.favorites.length">
      <li v-for="(course, i) in store.favorites" :key="i">{{ course }}</li>
    </ul>
  </div>
</template>

<script setup>
import { useFavoriteStore } from "../stores/favorite"; // ✅ import store

const store = useFavoriteStore(); // ✅ เรียกใช้งาน store
</script>

<style scoped>
.page-container {
  text-align: center;
  padding: 40px;
}
</style>
