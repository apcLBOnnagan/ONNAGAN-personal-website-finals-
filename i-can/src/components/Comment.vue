<!-- filepath: c:\Users\LENOVO\Documents\CODERISM\WHYYY\i-can\src\components\Comment.vue -->
<template>
    <div class="comment-container">
      <h1>Comments</h1>
      <ul>
        <li v-for="comment in comments" :key="comment.id">{{ comment.name }}: {{ comment.comment }}</li>
      </ul>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../lib/supabaseClient'

const comments = ref([])

async function getComments() {
  const { data, error } = await supabase.from('comments').select()
  if (error) {
    console.error("Error fetching comments:", error);
    return;
  }
  comments.value = data;
}

onMounted(() => {
  getComments()
})
</script>

<style scoped>
.comment-section {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  margin-bottom: 5px; /* Add bottom margin */
}

.comment-container {
  background-color: rgba(245, 245, 220, 0.8);
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 90%;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  border-bottom: 1px solid #eee;
  padding: 5px 0;
}
</style>