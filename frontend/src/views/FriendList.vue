<template>
  <div class="page-head">
    <div>
      <span class="eyebrow">{{ friends.length }} connected</span>
      <h1>Friends</h1>
    </div>
    <router-link to="/friends/requests" class="btn-ghost btn">Requests</router-link>
  </div>

  <div class="form-card compact-form">
    <div v-if="error" class="error-banner">{{ error }}</div>
    <div v-if="message" class="success-banner">{{ message }}</div>

    <div v-if="currentUser" class="user-id-card">
      <span class="user-id-label">Your ID</span>
      <strong>#{{ currentUser.id }}</strong>
    </div>

    <form @submit.prevent="send">
      <div class="field">
        <label>Send request by user ID</label>
        <input v-model="receiverId" type="number" min="1" placeholder="e.g. 201" required />
      </div>
      <button class="btn-block" :disabled="sending">{{ sending ? "Sending..." : "Send Friend Request" }}</button>
    </form>
  </div>

  <div v-if="loading" class="loading-state">Loading friends...</div>

  <div v-else-if="friends.length">
    <div v-for="f in friends" :key="f.id" class="card card-row">
      <div style="display:flex; align-items:center; gap:12px;">
        <div class="avatar">{{ initials(f.name) }}</div>
        <div>
          <h3 style="margin-bottom:2px;">{{ f.name }}</h3>
          <div style="display:flex; flex-wrap:wrap; gap:8px; align-items:center; margin-top:4px;">
            <span style="color: var(--color-text-muted); font-size: 13px;">{{ f.eco_points }} eco points</span>
            <span style="color: var(--color-clay); font-size: 13px; font-weight:600;">ID: {{ f.id }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div v-else class="empty-state">
    <div class="empty-icon">🤝</div>
    No friends yet — send a request to start tracking together.
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { getFriends, sendRequest } from "../api/friend";
import { me } from "../api/auth";
import { apiErrorMessage } from "../api/client";

const friends = ref([]);
const currentUser = ref(null);
const receiverId = ref("");
const loading = ref(true);
const sending = ref(false);
const error = ref("");
const message = ref("");

function initials(name) {
  return (name || "")
    .split(" ")
    .map((p) => p[0])
    .join("")
    .slice(0, 2)
    .toUpperCase();
}

async function load() {
  loading.value = true;
  error.value = "";
  try {
    const res = await getFriends();
    friends.value = res.data.friends ?? [];
  } catch (err) {
    error.value = apiErrorMessage(err, "Could not load friends.");
  } finally {
    loading.value = false;
  }
}

async function loadProfile() {
  try {
    const res = await me();
    currentUser.value = res.data ?? null;
  } catch {
    currentUser.value = null;
  }
}

async function send() {
  sending.value = true;
  error.value = "";
  message.value = "";

  try {
    await sendRequest({ receiver_id: parseInt(receiverId.value, 10) });
    receiverId.value = "";
    message.value = "Friend request sent.";
  } catch (err) {
    error.value = apiErrorMessage(err, "Could not send this friend request.");
  } finally {
    sending.value = false;
  }
}

onMounted(async () => {
  await load();
  await loadProfile();
});
</script>

<style scoped>
.compact-form{
  max-width:520px;
  margin-bottom:18px;
}

.user-id-card{
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:12px;
  background:var(--moss-soft);
  color:var(--forest);
  border:1px solid var(--border);
  border-radius:12px;
  padding:10px 12px;
  margin-bottom:12px;
  font-size:14px;
}

.user-id-label{
  color:var(--color-text-muted);
  font-size:12px;
  text-transform:uppercase;
  letter-spacing:0.08em;
}
</style>
