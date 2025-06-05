<template>
  <div
    class="min-h-screen bg-white flex flex-col items-center justify-center px-4 py-6 relative"
    style="
      background-image: url('/image/bg-auth.png');
      background-size: cover;
      background-position: center;
    "
  >
    <div class="absolute inset-0 bg-white opacity-93"></div>

    <!-- Card Utama -->
    <div
      class="relative w-full max-w-2xl bg-white shadow-2xl rounded-2xl overflow-hidden flex flex-col md:flex-row z-10"
    >
      <!-- Kolom Kiri: Gambar + Wave Overlay -->
      <div class="md:w-1/2 relative hidden md:block min-h-[320px]">
        <!-- 1. Gambar penuh -->
        <img
          src="/image/logo_web.png"
          alt="Background"
          class="w-full h-full object-cover"
        />

        <!-- 2. Overlay Putih Semi-Transparan -->
        <div class="absolute inset-0 bg-white opacity-10"></div>

        <!-- 3. SVG Wave Overlay dengan gradient Hijau→Biru -->
        <svg
          viewBox="0 0 1440 320"
          class="absolute inset-0 w-full h-full"
          preserveAspectRatio="none"
        >
          <!-- Definisi Gradient -->
          <defs>
            <linearGradient id="waveGradient" x1="0%" y1="0%" x2="100%" y2="0%">
              <stop offset="0%" stop-color="#16A34A" />
              <!-- hijau-600 -->
              <stop offset="100%" stop-color="#3B82F6" />
              <!-- blue-500 -->
            </linearGradient>
          </defs>

          <path
            fill="url(#waveGradient)"
            d="M0,224L48,224C96,224,192,224,288,213.3C384,203,480,181,576,176C672,171,768,181,864,186.7C960,192,1056,192,1152,186.7C1248,181,1344,171,1392,165.3L1440,160L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"
            opacity="0.7"
          ></path>
        </svg>
      </div>

      <!-- Kolom Kanan: Form Register + Overlay Putih -->
      <div class="w-full md:w-1/2 relative">
        <!-- Overlay putih semi‐transparan hanya di kolom kanan -->
        <div class="absolute inset-0 bg-white opacity-90 z-10"></div>

        <!-- Isi Form berada di atas overlay putih -->
        <div class="relative z-20 p-4">
          <h1
            class="text-2xl font-bold bg-gradient-to-r from-green-600 to-blue-600 bg-clip-text text-transparent text-center mb-3"
          >
            Daftar Akun
          </h1>
          <form @submit.prevent="handleRegister" class="space-y-3">
            <!-- Nama -->
            <div>
              <label for="name" class="block text-xs font-medium text-gray-700 mb-1">
                Nama
              </label>
              <div class="relative">
                <div
                  class="absolute inset-y-0 left-0 pl-2 flex items-center pointer-events-none"
                >
                  <UserIcon class="h-4 w-4 text-gray-400" />
                </div>
                <input
                  id="name"
                  type="text"
                  v-model="form.name"
                  placeholder="Masukkan nama"
                  class="w-full pl-8 pr-2 py-1.5 text-sm border border-blue-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-600 transition"
                  required
                />
              </div>
            </div>

            <!-- Email -->
            <div>
              <label for="email" class="block text-xs font-medium text-gray-700 mb-1">
                Email
              </label>
              <div class="relative">
                <div
                  class="absolute inset-y-0 left-0 pl-2 flex items-center pointer-events-none"
                >
                  <EnvelopeIcon class="h-4 w-4 text-gray-400" />
                </div>
                <input
                  id="email"
                  type="email"
                  v-model="form.email"
                  placeholder="Masukkan email"
                  class="w-full pl-8 pr-2 py-1.5 text-sm border border-blue-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-600 transition"
                  required
                />
              </div>
            </div>

            <!-- No. HP -->
            <div>
              <label for="no_hp" class="block text-xs font-medium text-gray-700 mb-1">
                No. HP
              </label>
              <div class="relative">
                <div
                  class="absolute inset-y-0 left-0 pl-2 flex items-center pointer-events-none"
                >
                  <PhoneIcon class="h-4 w-4 text-gray-400" />
                </div>
                <input
                  id="no_hp"
                  type="tel"
                  v-model="form.no_hp"
                  placeholder="08xxxxxxxxxx"
                  class="w-full pl-8 pr-2 py-1.5 text-sm border border-blue-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-600 transition"
                  required
                />
              </div>
            </div>

            <!-- Alamat -->
            <div>
              <label for="alamat" class="block text-xs font-medium text-gray-700 mb-1">
                Alamat
              </label>
              <div class="relative">
                <div
                  class="absolute inset-y-0 left-0 pl-2 flex items-center pointer-events-none"
                >
                  <MapPinIcon class="h-4 w-4 text-gray-400" />
                </div>
                <input
                  id="alamat"
                  type="text"
                  v-model="form.alamat"
                  placeholder="Masukkan alamat"
                  class="w-full pl-8 pr-2 py-1.5 text-sm border border-blue-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-600 transition"
                  required
                />
              </div>
            </div>

            <!-- Password -->
            <div>
              <label for="password" class="block text-xs font-medium text-gray-700 mb-1">
                Password
              </label>
              <div class="relative">
                <div
                  class="absolute inset-y-0 left-0 pl-2 flex items-center pointer-events-none"
                >
                  <LockClosedIcon class="h-4 w-4 text-gray-400" />
                </div>
                <input
                  :type="showPassword ? 'text' : 'password'"
                  id="password"
                  v-model="form.password"
                  placeholder="Masukkan password"
                  class="w-full pl-8 pr-8 py-1.5 text-sm border border-blue-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-600 transition"
                  required
                />
                <button
                  type="button"
                  @click="togglePassword"
                  class="absolute inset-y-0 right-0 pr-2 flex items-center text-gray-500"
                >
                  <EyeIcon v-if="!showPassword" class="h-4 w-4" />
                  <EyeSlashIcon v-else class="h-4 w-4" />
                </button>
              </div>
            </div>

            <!-- Checkbox Syarat & Ketentuan -->
            <div class="flex items-center space-x-2 text-xs">
              <input
                id="terms"
                type="checkbox"
                v-model="terms"
                class="h-3 w-3 text-green-600 border-gray-300 rounded focus:ring-green-500"
              />
              <label for="terms" class="text-gray-600">
                Saya setuju dengan
                <a href="#" class="text-green-600 hover:underline"
                  >Syarat dan Ketentuan</a
                >
              </label>
            </div>

            <!-- Tombol Daftar -->
            <button
              type="submit"
              :disabled="!terms"
              class="w-full py-1.5 bg-gradient-to-r from-green-600 to-blue-600 hover:from-green-500 hover:to-blue-500 text-white text-sm font-semibold rounded-lg transition disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Daftar
            </button>
            <!-- Link ke Login -->
            <div class="mt-2 text-xs text-gray-600 text-center">
              Sudah punya akun?
              <router-link
                to="/layanan-publik/auth/login"
                class="text-green-600 hover:underline"
                >Masuk</router-link
              >
            </div>
          </form>
        </div>
      </div>
    </div>

    <!-- Card Logo di bawah (tetap sama seperti sebelumnya) -->
    <div class="mt-4 flex flex-wrap justify-center gap-3 z-10">
      <div
        class="w-16 h-16 bg-white rounded-xl shadow-md flex items-center justify-center"
      >
        <img
          src="/image/bmb.png"
          alt="Melasti"
          class="max-h-8 max-w-full object-contain p-1"
        />
      </div>
      <div
        class="w-16 h-16 bg-white rounded-xl shadow-md flex items-center justify-center"
      >
        <img
          src="/image/berakhlak.png"
          alt="Pusaka"
          class="max-h-8 max-w-full object-contain p-1"
        />
      </div>
      <div
        class="w-16 h-16 bg-white rounded-xl shadow-md flex items-center justify-center"
      >
        <img
          src="/image/melasti.png"
          alt="Simdiklat"
          class="max-h-8 max-w-full object-contain p-1"
        />
      </div>
      <div
        class="w-16 h-16 bg-white rounded-xl shadow-md flex items-center justify-center"
      >
        <img
          src="/image/susila.png"
          alt="Simpati"
          class="max-h-8 max-w-full object-contain p-1"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";
import Swal from "sweetalert2";

import {
  UserIcon,
  EnvelopeIcon,
  LockClosedIcon,
  EyeIcon,
  EyeSlashIcon,
  PhoneIcon,
  MapPinIcon,
} from "@heroicons/vue/24/outline";

const router = useRouter();
const terms = ref(false);

const form = reactive({
  name: "",
  email: "",
  no_hp: "",
  alamat: "",
  password: "",
});

const showPassword = ref(false);
function togglePassword() {
  showPassword.value = !showPassword.value;
}

const handleRegister = async () => {
  if (!form.name || !form.email || !form.no_hp || !form.alamat || !form.password) {
    Swal.fire({
      icon: "warning",
      title: "Data Kurang Lengkap",
      text: "Silakan isi semua field sebelum mendaftar.",
    });
    return;
  }

  const API_URL = import.meta.env.VITE_API_URL;

  try {
    const response = await axios.post(`${API_URL}/register`, {
      name: form.name,
      email: form.email,
      no_hp: form.no_hp,
      alamat: form.alamat,
      password: form.password,
    });
    const result = response.data;

    if (result.status === 201 || result.status === 200) {
      await Swal.fire({
        icon: "success",
        title: "Berhasil Mendaftar",
        text: "Anda akan dialihkan ke halaman Masuk.",
        timer: 1500,
        showConfirmButton: false,
      });
      router.push({ name: "Login" });
    }
  } catch (error) {
    console.error(error);
    Swal.fire({
      icon: "error",
      title: "Pendaftaran Gagal",
      text: error.response?.data?.message || "Terjadi kesalahan pada server.",
    });
  }
};
</script>

<style scoped>
/* Kelas kustom untuk gradient border pada focus */
.focus\:bg-gradient-border:focus {
  border-color: transparent !important;
  background-image: linear-gradient(white, white),
    linear-gradient(to right, #16a34a, #3b82f6);
  background-origin: padding-box, border-box;
  background-clip: padding-box, border-box;
}
</style>
