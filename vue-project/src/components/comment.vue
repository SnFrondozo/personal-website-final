<template>
  <div id="comments" class="container guestbook-container">
    <div class="header">
      <div class="title-container">Comments</div>
    </div>
    <form @submit.prevent="addComment">
      <div>
        <p>
          Name: <br />
          <input type="text" v-model="guestName" placeholder="Enter your name" required />
        </p>
        <p>
          Comment: <br />
          <textarea v-model="guestComment" placeholder="Write your comment" rows="4" required></textarea>
        </p>
        <button type="submit">Submit</button>
      </div>
    </form>
    <div class="comment-section">
      <div v-for="comment in comments" :key="comment.id" class="comment">
        <p><strong>{{ comment.name }}</strong></p>
        <p>{{ comment.message }}</p>
      </div>
    </div>
  </div>
</template>

<style>
body {
  background-color: #020202;
}

.comment-section {
  margin-top: 20px;
  text-align: left;
}

.comment {
  border-top: 1px solid #ddd;
  padding: 10px 0;
}

.comment p {
  margin: 5px 0;
}

.guestbook-container {
  background-color: #ff4444;
  border: 2px solid #562123;
  padding: 20px;
  border-radius: 10px;
  max-width: 800px;
  margin: 0 auto;
}

.guestbook-container .header {
  text-align: center;
  margin-bottom: 20px;
}

.guestbook-container .header .title-container {
  font-size: 24px;
  font-weight: bold;
  color: #562123;
}

.guestbook-container form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.guestbook-container input,
.guestbook-container textarea {
  padding: 10px;
  border: 1px solid #562123;
  border-radius: 5px;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
}

.guestbook-container button {
  background-color: #d1b7b7;
  color: #030303;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.guestbook-container button:hover {
  background-color: #6c3a32;
}
</style>

<script setup>
import { ref, onMounted } from 'vue';
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = "https://pbgrtsnznubwycohnljl.supabase.co";
const supabaseAnonKey = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InBiZ3J0c256bnVid3ljb2hubGpsIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDA3MzE5NzMsImV4cCI6MjA1NjMwNzk3M30.sxiaO9Dmf9yFM52slmYDXeX-XjNDFC-_zErsgxdnCQ8";
const supabase = createClient(supabaseUrl, supabaseAnonKey);

const guestName = ref('');
const guestComment = ref('');
const comments = ref([]);

// Fetch existing comments on load
const fetchComments = async () => {
  const { data, error } = await supabase.from('comments').select('*').order('created_at', { ascending: false });
  if (error) console.error(error);
  else comments.value = data;
};

onMounted(fetchComments);

// Add new comment
const addComment = async () => {
  if (!guestName.value || !guestComment.value) return;

  const name = guestName.value;
  const message = guestComment.value;

  // Reset input fields immediately
  guestName.value = '';
  guestComment.value = '';

  const { error } = await supabase.from('comments').insert([{ name, message }]);

  if (error) {
    console.error(error);
  } else {
    fetchComments(); // Refresh comments list
  }
};
</script>
