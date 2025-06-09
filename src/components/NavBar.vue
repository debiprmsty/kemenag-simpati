<template>
  <!-- NAVBAR UTAMA -->
  <nav
    class="w-full mt-4 md:max-w-[94vw] max-w-[92vw] mx-auto px-4 py-3 bg-white border border-gray-300 rounded-2xl shadow-md flex items-center justify-between z-10"
  >
    <!-- Logo -->
    <div class="flex items-center space-x-2">
      <router-link to="/" class="flex gap-2">
        <img src="/image/logo_web.png" alt="Logo" class="h-8 hover:cursor-pointer" />
        <span class="text-gray-900 font-semibold text-lg hover:cursor-pointer mt-0.5">
          SIMPATI
        </span>
      </router-link>
    </div>

    <!-- Mid Menu (desktop only) -->
    <div class="hidden md:flex items-center space-x-6">
      <!-- Beranda -->
      <router-link
        to="/"
        class="px-3 py-2 rounded-2xl font-semibold text-gray-800 hover:text-green-600 hover:bg-[#D5E3DA] transition"
        :class="{
          'bg-[#D5E3DA] border border-[#C4DAD2] text-green-600': isActiveRoute('/'),
          'bg-transparent border border-transparent': !isActiveRoute('/'),
        }"
      >
        Beranda
      </router-link>

      <!-- FAQ -->
      <router-link
        to="/faq"
        class="px-3 py-2 rounded-2xl font-semibold text-gray-800 hover:text-green-600 hover:bg-[#D5E3DA] transition"
        :class="{
          'bg-[#D5E3DA] border border-[#C4DAD2] text-green-600': isActiveRoute('/faq'),
          'bg-transparent border border-transparent': !isActiveRoute('/faq'),
        }"
      >
        FAQ
      </router-link>

      <!-- Pengaduan Publik (dropdown parent) -->
      <div class="relative">
        <button
          @click="togglePengaduanDropdown"
          class="inline-flex items-center hover:cursor-pointer space-x-1 px-3 py-2 rounded-2xl font-medium text-gray-800 hover:text-green-600 hover:bg-[#D5E3DA] transition"
          :class="{
            'bg-[#D5E3DA] border border-[#C4DAD2] text-green-600':
              isActiveRoute('/sp4n-lapor') || isActiveRoute('/whatsapp-center'),
            'bg-transparent border border-transparent': !(
              isActiveRoute('/sp4n-lapor') || isActiveRoute('/whatsapp-center')
            ),
          }"
        >
          <span>Pengaduan Publik</span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-4 w-4"
            fill="currentColor"
            viewBox="0 0 20 20"
          >
            <path
              d="M5.23 7.21a.75.75 0 011.06.02L10 10.98l3.71-3.75a.75.75
                 0 011.08 1.04l-4.24 4.29a.75.75 0 01-1.06 0L5.23
                 8.27a.75.75 0 01.02-1.06z"
            />
          </svg>
        </button>

        <!-- Dropdown untuk Pengaduan Publik -->
        <div
          v-if="pengaduanDropdownOpen"
          class="absolute right-0 mt-2 bg-white border border-gray-100 rounded-xl shadow-lg w-44 z-20"
        >
          <router-link
            to="/sp4n-lapor"
            class="block px-4 py-2 text-gray-700 hover:text-gray-900 hover:bg-[#E9EFEC] rounded-xl transition"
            :class="{ 'bg-[#E9EFEC]': isActiveRoute('/sp4n-lapor') }"
            @click="pengaduanDropdownOpen = false"
          >
            SP4N Lapor
          </router-link>
          <a
            href="https://wa.me/+6285928877957"
            class="block px-4 py-2 text-gray-700 hover:text-gray-900 hover:bg-[#E9EFEC] rounded-xl transition"
            :class="{ 'bg-[#E9EFEC]': isActiveRoute('/whatsapp-center') }"
            @click="pengaduanDropdownOpen = false"
          >
            WhatsApp Center
          </a>
        </div>
      </div>
    </div>

    <!-- Bagian kanan (Auth / Profil) -->
    <div class="hidden md:flex items-center space-x-4">
      <!-- Tombol Masuk / Daftar -->
      <router-link
        v-if="!isLoggedIn"
        to="/layanan-publik/auth/login"
        class="font-semibold text-gray-800 hover:text-[#16423C] transition"
      >
        Masuk
      </router-link>
      <router-link
        v-if="!isLoggedIn"
        to="/layanan-publik/auth/register"
        class="px-4 py-2 bg-[#1B4D3E] text-white rounded-2xl hover:bg-[#16423C] font-semibold transition"
      >
        Daftar
      </router-link>

      <!-- Profil dan Logout -->
      <div v-if="isLoggedIn" class="relative">
        <button
          @click="toggleProfileDropdown"
          ref="profileDropdownButton"
          class="flex items-center space-x-2 group focus:outline-none"
        >
          <span
            v-if="user.name"
            class="text-gray-800 font-medium group-hover:text-[#16423C] transition"
          >
            {{ user.name }}
          </span>
          <img
            :src="user.avatarUrl"
            alt="Avatar"
            class="h-8 w-8 rounded-full hover:cursor-pointer border-2 border-gray-300 group-hover:border-[#16423C] transition"
          />
        </button>
        <div
          v-if="profileDropdownOpen"
          ref="profileDropdownContent"
          class="absolute right-0 mt-2 w-48 bg-white rounded-xl shadow-lg border border-gray-100 z-20 py-1"
        >
          <router-link
            to="/profile"
            class="block px-4 py-2 text-sm text-gray-700 hover:text-gray-900 hover:bg-[#E9EFEC] transition"
            @click="profileDropdownOpen = false"
          >
            Profil Saya
          </router-link>
          <router-link
            to="/list-satker#me-progress"
            class="block px-4 py-2 text-sm text-gray-700 hover:text-gray-900 hover:bg-[#E9EFEC] transition"
            @click="profileDropdownOpen = false"
          >
            Pengajuan Saya
          </router-link>
          <button
            @click="triggerLogoutConfirmation"
            class="w-full text-left block px-4 py-2 text-sm text-gray-700 hover:text-red-600 hover:bg-[#E9EFEC] transition"
          >
            Logout
          </button>
        </div>
      </div>
    </div>

    <!-- Tombol Hamburger (mobile) -->
    <button @click="mobileOpen = !mobileOpen" class="md:hidden text-gray-800">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"
        />
      </svg>
    </button>
  </nav>

  <!-- MOBILE MENU -->
  <div
    v-if="mobileOpen"
    class="md:hidden bg-white border-t border-gray-200 shadow-md mx-4 rounded-xl"
  >
    <!-- Link Beranda -->
    <router-link
      to="/"
      class="block px-4 py-2 font-semibold text-gray-800 hover:bg-gray-100 transition"
      @click="mobileOpen = false"
    >
      Beranda
    </router-link>

    <!-- Link FAQ -->
    <router-link
      to="/faq"
      class="block px-4 py-2 font-semibold text-gray-800 hover:bg-gray-100 transition"
      @click="mobileOpen = false"
    >
      FAQ
    </router-link>

    <!-- Dropdown Pengaduan Publik -->
    <div class="border-t border-gray-100">
      <button
        @click.stop="togglePengaduanDropdown"
        ref="pengaduanDropdownButton"
        class="w-full flex justify-between items-center px-4 py-2 font-semibold text-gray-800 hover:bg-gray-100 transition"
      >
        <span>Pengaduan Publik</span>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 transition-transform"
          :class="{ 'rotate-180': pengaduanDropdownOpen }"
          fill="currentColor"
          viewBox="0 0 20 20"
        >
          <path
            d="M5.23 7.21a.75.75 0 011.06.02L10 10.98l3.71-3.75a.75.75 0 011.08 1.04l-4.24 4.29a.75.75 
               0 01-1.06 0L5.23 8.27a.75.75 0 01.02-1.06z"
          />
        </svg>
      </button>
      <div
        v-if="pengaduanDropdownOpen"
        ref="pengaduanDropdownContent"
        class="pl-4 border-t border-gray-100"
      >
        <router-link
          to="/sp4n-lapor"
          class="block px-4 py-2 font-medium text-gray-700 hover:bg-[#E9EFEC] rounded-xl transition"
          @click="
            mobileOpen = false;
            pengaduanDropdownOpen = false;
          "
        >
          SP4N Lapor
        </router-link>
        <a
          href="https://wa.me/+6285928877957"
          class="block px-4 py-2 font-medium text-gray-700 hover:bg-[#E9EFEC] rounded-xl transition"
          @click="
            mobileOpen = false;
            pengaduanDropdownOpen = false;
          "
        >
          WhatsApp Center
        </a>
      </div>
    </div>

    <!-- Auth (Masuk / Daftar) -->
    <div v-if="!isLoggedIn" class="border-t border-gray-100">
      <router-link
        to="/layanan-publik/auth/login"
        class="block px-4 py-2 font-semibold text-gray-800 hover:bg-gray-100 transition"
        @click="mobileOpen = false"
      >
        Masuk
      </router-link>
      <router-link
        to="/layanan-publik/auth/register"
        class="block mx-4 my-2 px-4 py-2 text-center bg-[#1B4D3E] text-white rounded-2xl font-semibold hover:bg-[#16423C] transition"
        @click="mobileOpen = false"
      >
        Daftar
      </router-link>
    </div>

    <!-- Profil & Logout (jika sudah login) -->
    <div v-if="isLoggedIn" class="border-t border-gray-100">
      <button
        @click="toggleProfileDropdown"
        ref="profileMobileDropdownButton"
        class="w-full flex justify-between items-center px-4 py-3 group"
      >
        <div class="flex items-center space-x-3">
          <img
            :src="user.avatarUrl || '/image/cartoon.png'"
            alt="Avatar"
            class="h-10 w-10 hover:cursor-pointer rounded-full border-2 border-gray-300 group-hover:border-[#16423C] transition"
          />
          <span
            v-if="user.name"
            class="text-gray-800 font-semibold group-hover:text-[#16423C] transition"
          >
            {{ user.name }}
          </span>
        </div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 transition-transform"
          :class="{ 'rotate-180': profileDropdownOpen }"
          fill="currentColor"
          viewBox="0 0 20 20"
        >
          <path
            d="M5.23 7.21a.75.75 0 011.06.02L10 10.98l3.71-3.75a.75.75 0 011.08 1.04l-4.24 4.29a.75.75 
               0 01-1.06 0L5.23 8.27a.75.75 0 01.02-1.06z"
          />
        </svg>
      </button>

      <!-- Dropdown Profil Mobile -->
      <div
        v-if="profileDropdownOpen"
        ref="profileMobileDropdownContent"
        class="pl-4 border-t border-gray-100"
      >
        <router-link
          to="/profile"
          class="block px-4 py-2 text-sm text-gray-700 hover:bg-[#E9EFEC] transition"
          @click="
            mobileOpen = false;
            profileDropdownOpen = false;
          "
        >
          Profil Saya
        </router-link>
        <router-link
          to="/list-satker#me-progress"
          class="block px-4 py-2 text-sm text-gray-700 hover:bg-[#E9EFEC] transition"
          @click="
            mobileOpen = false;
            profileDropdownOpen = false;
          "
        >
          Pengajuan Saya
        </router-link>
      </div>

      <button
        @click="handleMobileLogout"
        class="w-full text-left block px-4 py-2 font-semibold text-gray-800 hover:bg-gray-100 hover:text-red-500 transition"
      >
        Logout
      </button>
    </div>
  </div>

  <!-- MODAL KONFIRMASI LOGOUT -->
  <div
    v-if="showLogoutConfirmModal"
    class="fixed inset-0 bg-transparent backdrop-blur-sm flex items-center justify-center z-50 p-4"
  >
    <div class="bg-white p-6 rounded-lg shadow-xl max-w-sm w-full">
      <h3 class="text-lg font-semibold mb-4 text-gray-900">Konfirmasi Logout</h3>
      <p class="text-gray-700 mb-6">Apakah Anda yakin ingin keluar?</p>
      <div class="flex justify-end space-x-3">
        <button
          @click="cancelLogout"
          class="px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300 transition"
        >
          Batal
        </button>
        <button
          @click="executeLogout"
          class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition"
        >
          Ya, Logout
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import { useRouter, useRoute } from "vue-router";

const mobileOpen = ref(false);
const pengaduanDropdownOpen = ref(false);
const profileDropdownOpen = ref(false);
const showLogoutConfirmModal = ref(false);

const route = useRoute();
const router = useRouter();
const apiUrl = import.meta.env.VITE_API_URL;

const isLoggedIn = ref(false);
const user = ref({
  avatarUrl: "",
  name: null,
});

// Utility untuk cek active route
function isActiveRoute(path) {
  return route.path === path;
}

// Fetch data user jika ada token
async function fetchUserData(token) {
  try {
    const response = await fetch(`${apiUrl}/me`, {
      method: "GET",
      headers: {
        Authorization: `Bearer ${token}`,
        Accept: "application/json",
      },
    });
    if (response.ok) {
      const data = await response.json();
      user.value.name = data.data.name;
      user.value.avatarUrl = data.data.avatar
        ? `${apiUrl}/my-avatar/${data.data.avatar}`
        : localStorage.getItem("avatarUrl") || "/image/cartoon.png";
    } else if (response.status === 401) {
      await performClientSideLogout();
      router.push("/layanan-publik/auth/login");
    }
  } catch (error) {
    console.error("Error fetching user data:", error);
  }
}

// Logout lokal
async function performClientSideLogout() {
  localStorage.removeItem("token");
  localStorage.removeItem("avatarUrl");
  isLoggedIn.value = false;
  user.value = { avatarUrl: "", name: null };
  profileDropdownOpen.value = false;
  pengaduanDropdownOpen.value = false;
  mobileOpen.value = false;
}

// Eksekusi logout via API lalu lokal
async function executeLogout() {
  showLogoutConfirmModal.value = false;
  const token = localStorage.getItem("token");
  if (token && apiUrl) {
    try {
      await fetch(`${apiUrl}/logout`, {
        method: "POST",
        headers: {
          Authorization: `Bearer ${token}`,
          Accept: "application/json",
        },
      });
    } catch (error) {
      console.warn("API logout request failed:", error);
    }
  }
  await performClientSideLogout();
  router.push("/layanan-publik/auth/login");
}

// Modal control
function cancelLogout() {
  showLogoutConfirmModal.value = false;
}
function triggerLogoutConfirmation() {
  profileDropdownOpen.value = false;
  showLogoutConfirmModal.value = true;
}
function handleMobileLogout() {
  mobileOpen.value = false;
  triggerLogoutConfirmation();
}

// Dropdown toggles
function togglePengaduanDropdown() {
  pengaduanDropdownOpen.value = !pengaduanDropdownOpen.value;
  profileDropdownOpen.value = false;
}
function toggleProfileDropdown() {
  profileDropdownOpen.value = !profileDropdownOpen.value;
  if (profileDropdownOpen.value) pengaduanDropdownOpen.value = false;
}

// Refs untuk elemen dropdown
const pengaduanDropdownButton = ref(null);
const pengaduanDropdownContent = ref(null);
const profileDropdownButton = ref(null);
const profileDropdownContent = ref(null);
const profileMobileDropdownButton = ref(null);
const profileMobileDropdownContent = ref(null);

// === Event handler named functions ===

// Klik di luar dropdown → tutup dropdown manapun yang open
function handleClickOutside(event) {
  // Pengaduan (desktop & mobile)
  if (
    pengaduanDropdownOpen.value &&
    pengaduanDropdownButton.value &&
    !pengaduanDropdownButton.value.contains(event.target) &&
    pengaduanDropdownContent.value &&
    !pengaduanDropdownContent.value.contains(event.target)
  ) {
    pengaduanDropdownOpen.value = false;
  }

  // Profil (desktop & mobile)
  if (profileDropdownOpen.value) {
    const isDeskBtn = profileDropdownButton.value?.contains(event.target);
    const isDeskContent = profileDropdownContent.value?.contains(event.target);
    const isMobBtn = profileMobileDropdownButton.value?.contains(event.target);
    const isMobContent = profileMobileDropdownContent.value?.contains(event.target);
    if (!isDeskBtn && !isDeskContent && !isMobBtn && !isMobContent) {
      profileDropdownOpen.value = false;
    }
  }
}

// Storage event → reload user jika ada update
function handleStorageChange(e) {
  if (e.key === "profile_updated") {
    const token = localStorage.getItem("token");
    if (token) fetchUserData(token);
  }
}

// Custom event 'profile-updated' → update user data
function handleProfileUpdated(event) {
  const updatedUser = event.detail;
  user.value.name = updatedUser.name;
  if (updatedUser.avatar) {
    const newAvatarUrl = `${apiUrl}/my-avatar/${updatedUser.avatar}`;
    user.value.avatarUrl = newAvatarUrl;
    localStorage.setItem("avatarUrl", newAvatarUrl);
  }
}

onMounted(() => {
  const token = localStorage.getItem("token");
  isLoggedIn.value = !!token;
  if (isLoggedIn.value) {
    user.value.avatarUrl = localStorage.getItem("avatarUrl") || "/image/cartoon.png";
    fetchUserData(token);
  }

  // Daftarkan semua listener dengan named functions
  window.addEventListener("storage", handleStorageChange);
  window.addEventListener("click", handleClickOutside);
  window.addEventListener("profile-updated", handleProfileUpdated);
});

onBeforeUnmount(() => {
  // Hapus listener dengan dua argumen
  window.removeEventListener("storage", handleStorageChange);
  window.removeEventListener("click", handleClickOutside);
  window.removeEventListener("profile-updated", handleProfileUpdated);
});
</script>

<style>
.rotate-180 {
  transform: rotate(180deg);
}

/* Pastikan navbar selalu di atas konten lain */
nav {
  z-index: 999;
}
</style>
