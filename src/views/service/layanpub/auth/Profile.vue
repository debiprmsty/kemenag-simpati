<template>
  <div class="min-h-screen bg-gray-50 relative overflow-hidden">
    <!-- Animated background elements -->
    <div class="absolute inset-0 opacity-10">
      <div
        class="absolute top-20 left-20 w-40 h-40 bg-gradient-to-br from-green-500 to-blue-600 rounded-full blur-2xl animate-float"
      ></div>
      <div
        class="absolute bottom-32 right-32 w-32 h-32 bg-gradient-to-br from-green-600 to-blue-600 rounded-full blur-xl animate-float-delayed"
      ></div>
      <div
        class="absolute top-1/2 left-10 w-24 h-24 bg-gradient-to-br from-green-700 to-blue-700 rounded-full blur-xl animate-float-slow"
      ></div>
    </div>

    <!-- Geometric patterns -->
    <div class="absolute inset-0 opacity-5">
      <div class="absolute top-0 left-0 w-full h-full">
        <svg class="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
          <defs>
            <pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse">
              <path
                d="M 10 0 L 0 0 0 10"
                fill="none"
                stroke="currentColor"
                stroke-width="0.5"
              />
            </pattern>
          </defs>
          <rect width="100" height="100" fill="url(#grid)" class="text-gray-400" />
        </svg>
      </div>
    </div>

    <!-- Floating particles -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        v-for="i in 20"
        :key="i"
        class="absolute w-1 h-1 bg-gradient-to-r from-green-600 to-blue-600 rounded-full animate-ping"
        :style="{
          left: Math.random() * 100 + '%',
          top: Math.random() * 100 + '%',
          animationDelay: Math.random() * 3 + 's',
          animationDuration: 2 + Math.random() * 2 + 's',
        }"
      ></div>
    </div>

    <div class="mx-auto md:max-w-[94vw] max-w-[92vw] md:my-12 my-6 relative z-10">
      <!-- Header -->
      <div class="text-center mb-16">
        <div
          class="inline-flex items-center justify-center md:w-20 md:h-20 w-12 h-12 bg-gradient-to-br from-green-600 to-blue-600 rounded-2xl md:mb-6 mb-4 shadow-2xl"
        >
          <User class="md:w-10 md:h-10 w-7 h-7 text-white" />
        </div>
        <h1 class="text-4xl md:text-6xl font-black text-slate-800 mb-2 tracking-tight">
          PROFIL SAYA
        </h1>
        <p class="text-gray-600 md:text-xl text-md font-medium">
          Sesuaikan profil Anda agar tetap akurat dan terkini.
        </p>
        <div class="flex items-center justify-center md:mt-6 mt-4">
          <div
            class="w-32 h-1 bg-gradient-to-r from-green-600 to-blue-600 rounded-full"
          ></div>
        </div>
      </div>

      <!-- Main content -->
      <div class="w-full mx-auto md:-mt-5 -mt-8">
        <div
          class="bg-white/80 backdrop-blur-xl border-2 border-gray-200/50 rounded-3xl p-5 md:p-8 shadow-2xl shadow-blue-500/10 relative overflow-hidden"
        >
          <!-- Decorative elements -->
          <div
            class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-blue-500/10 to-purple-500/10 rounded-full blur-2xl"
          ></div>
          <div
            class="absolute bottom-0 left-0 w-24 h-24 bg-gradient-to-br from-cyan-500/10 to-blue-500/10 rounded-full blur-xl"
          ></div>

          <!-- Profile Image Section -->
          <div class="text-center md:mb-10 mb-5">
            <h2
              class="md:text-3xl text-xl md:font-bold font-medium text-gray-900 md:mb-8 mb-4 flex items-center justify-center space-x-3"
            >
              <div
                class="md:w-8 md:h-8 w-6 h-6 bg-gradient-to-br from-green-600 to-blue-600 rounded-lg flex items-center justify-center"
              >
                <User class="md:w-5 md:h-5 w-4 h-4 text-white" />
              </div>
              <span>Edit Profile</span>
            </h2>

            <div class="relative inline-block group">
              <!-- Profile image container -->
              <div class="text-center mb-5">
                <div class="relative inline-block group">
                  <!-- Kotak lingkaran untuk foto profil -->
                  <div class="relative w-32 h-32 md:w-40 md:h-40 mx-auto">
                    <div
                      class="w-full h-full rounded-full bg-gradient-to-br from-green-600 to-blue-600 p-1 animate-pulse"
                    >
                      <div
                        class="w-full h-full rounded-full overflow-hidden bg-slate-800 flex items-center justify-center"
                      >
                        <!-- Tampilkan gambar jika ada, kalau belum tampilkan ikon user -->
                        <img
                          v-if="profileImageUrl"
                          :src="profileImageUrl"
                          class="w-full h-full object-cover rounded-full"
                        />
                        <User v-else class="w-16 h-16 text-gray-400" />
                      </div>
                    </div>

                    <!-- Overlay untuk upload -->
                    <div
                      class="absolute inset-0 rounded-full bg-black/50 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center"
                    >
                      <Camera class="w-8 h-8 text-white" />
                    </div>

                    <!-- Tombol edit gambar -->
                    <button
                      @click="triggerImageUpload"
                      class="absolute bottom-2 right-2 w-10 h-10 bg-gradient-to-r from-green-600 to-blue-600 rounded-full flex items-center justify-center hover:scale-110 transition-transform duration-300 shadow-lg"
                    >
                      <Edit class="w-5 h-5 text-white" />
                    </button>
                  </div>

                  <!-- Input file tersembunyi -->
                  <input
                    ref="fileInput"
                    type="file"
                    accept="image/*"
                    @change="handleImageUpload"
                    class="hidden"
                  />
                </div>

                <p class="text-gray-500 md:text-md text-sm md:mt-4 mt-3 md:font-medium">
                  Klik tombol edit untuk mengunggah foto profil baru
                </p>
              </div>
            </div>
          </div>

          <!-- Form Section -->
          <form @submit.prevent="saveProfile" class="md:space-y-7 space-y-4">
            <!-- Two Column Layout -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-5 lg:gap-12">
              <!-- Kolom kiri: Nama, Email, Alamat -->
              <div class="md:space-y-8 space-y-5">
                <!-- Nama Lengkap -->
                <div class="space-y-1">
                  <label
                    class="flex items-center text-gray-800 font-semibold text-[1rem]"
                  >
                    Nama Lengkap
                  </label>
                  <div class="relative">
                    <div class="absolute left-4 top-1/2 transform -translate-y-1/2">
                      <UserCheck class="md:w-4.5 md:h-4.5 w-4 h-4 text-[#16423C]" />
                    </div>
                    <input
                      v-model="profile.name"
                      type="text"
                      placeholder="Masukkan nama lengkap Anda"
                      class="w-full bg-gray-white rounded-xl pl-12 py-2 px-4 text-m text-green-950 placeholder-gray-500 focus:outline-none focus:bg-gradient-border border-[1.5px] border-gray-500"
                      :class="{
                        'border-red-400 focus:border-red-400 focus:ring-red-400/20':
                          errors.name,
                      }"
                    />
                  </div>
                  <p v-if="errors.name" class="text-red-500 text-sm md:font-medium">
                    {{ errors.name }}
                  </p>
                </div>

                <!-- Email -->
                <div class="space-y-1">
                  <label
                    class="flex items-center text-gray-800 font-semibold text-[1rem]"
                  >
                    Alamat Email
                  </label>
                  <div class="relative">
                    <div class="absolute left-4 top-1/2 transform -translate-y-1/2">
                      <Mail class="md:w-4.5 md:h-4.5 w-4 h-4 text-[#16423C]" />
                    </div>
                    <input
                      v-model="profile.email"
                      type="email"
                      placeholder="Masukkan alamat email Anda"
                      class="w-full bg-gray-white rounded-xl pl-12 py-2 px-4 text-m text-green-950 placeholder-gray-500 focus:outline-none focus:bg-gradient-border border-[1.5px] border-gray-500"
                      :class="{
                        'border-red-400 focus:border-red-400 focus:ring-red-400/20':
                          errors.email,
                      }"
                    />
                  </div>
                  <p v-if="errors.email" class="text-red-500 text-sm md:font-medium">
                    {{ errors.email }}
                  </p>
                </div>

                <!-- Alamat -->
                <div class="space-y-1">
                  <label
                    class="flex items-center text-gray-800 font-semibold text-[1rem]"
                  >
                    Alamat
                  </label>
                  <div class="relative">
                    <div class="absolute left-4 top-1/2 transform -translate-y-1/2">
                      <MapPinHouseIcon class="md:w-4.5 md:h-4.5 w-4 h-4 text-[#16423C]" />
                    </div>
                    <input
                      v-model="profile.alamat"
                      type="text"
                      placeholder="Masukkan alamat tempat tinggal Anda"
                      class="w-full bg-gray-white rounded-xl pl-12 py-2 px-4 text-m text-green-950 placeholder-gray-500 focus:outline-none focus:bg-gradient-border border-[1.5px] border-gray-500"
                      :class="{
                        'border-red-400 focus:border-red-400 focus:ring-red-400/20':
                          errors.alamat,
                      }"
                    />
                    <div
                      class="absolute inset-0 md:rounded-2xl rounded-xl bg-gradient-to-r from-indigo-500/0 to-indigo-500/0 group-hover:from-indigo-500/5 group-hover:to-indigo-500/5 transition-all duration-300 pointer-events-none"
                    ></div>
                  </div>
                  <p v-if="errors.alamat" class="text-red-500 text-sm md:font-medium">
                    {{ errors.alamat }}
                  </p>
                </div>
              </div>

              <!-- Kolom kanan: WhatsApp dan Password -->
              <div class="md:space-y-8 space-y-5">
                <!-- Nomor WhatsApp -->
                <div class="space-y-1">
                  <label
                    class="flex items-center text-gray-800 font-semibold text-[1rem]"
                  >
                    Nomor WhatsApp
                  </label>
                  <div class="relative">
                    <div
                      class="absolute left-4 top-1/2 transform -translate-y-1/2 text-blue-400"
                    >
                      <svg
                        class="h-5 w-5"
                        xmlns="http://www.w3.org/2000/svg"
                        x="0px"
                        y="0px"
                        width="100"
                        height="100"
                        viewBox="0,0,256,256"
                      >
                        <g
                          fill="#16423c"
                          fill-rule="nonzero"
                          stroke="none"
                          stroke-width="1"
                          stroke-linecap="butt"
                          stroke-linejoin="miter"
                          stroke-miterlimit="10"
                          stroke-dasharray=""
                          stroke-dashoffset="0"
                          font-family="none"
                          font-weight="none"
                          font-size="none"
                          text-anchor="none"
                          style="mix-blend-mode: normal"
                        >
                          <g transform="scale(5.12,5.12)">
                            <path
                              d="M25,2c-12.69047,0 -23,10.30953 -23,23c0,4.0791 1.11869,7.88588 2.98438,11.20898l-2.94727,10.52148c-0.09582,0.34262 -0.00241,0.71035 0.24531,0.96571c0.24772,0.25536 0.61244,0.35989 0.95781,0.27452l10.9707,-2.71875c3.22369,1.72098 6.88165,2.74805 10.78906,2.74805c12.69047,0 23,-10.30953 23,-23c0,-12.69047 -10.30953,-23 -23,-23zM25,4c11.60953,0 21,9.39047 21,21c0,11.60953 -9.39047,21 -21,21c-3.72198,0 -7.20788,-0.97037 -10.23828,-2.66602c-0.22164,-0.12385 -0.48208,-0.15876 -0.72852,-0.09766l-9.60742,2.38086l2.57617,-9.19141c0.07449,-0.26248 0.03851,-0.54399 -0.09961,-0.7793c-1.84166,-3.12289 -2.90234,-6.75638 -2.90234,-10.64648c0,-11.60953 9.39047,-21 21,-21zM16.64258,13c-0.64104,0 -1.55653,0.23849 -2.30859,1.04883c-0.45172,0.48672 -2.33398,2.32068 -2.33398,5.54492c0,3.36152 2.33139,6.2621 2.61328,6.63477h0.00195v0.00195c-0.02674,-0.03514 0.3578,0.52172 0.87109,1.18945c0.5133,0.66773 1.23108,1.54472 2.13281,2.49414c1.80347,1.89885 4.33914,4.09336 7.48633,5.43555c1.44932,0.61717 2.59271,0.98981 3.45898,1.26172c1.60539,0.5041 3.06762,0.42747 4.16602,0.26563c0.82216,-0.12108 1.72641,-0.51584 2.62109,-1.08203c0.89469,-0.56619 1.77153,-1.2702 2.1582,-2.33984c0.27701,-0.76683 0.41783,-1.47548 0.46875,-2.05859c0.02546,-0.29156 0.02869,-0.54888 0.00977,-0.78711c-0.01897,-0.23823 0.0013,-0.42071 -0.2207,-0.78516c-0.46557,-0.76441 -0.99283,-0.78437 -1.54297,-1.05664c-0.30567,-0.15128 -1.17595,-0.57625 -2.04883,-0.99219c-0.8719,-0.41547 -1.62686,-0.78344 -2.0918,-0.94922c-0.29375,-0.10568 -0.65243,-0.25782 -1.16992,-0.19922c-0.51749,0.0586 -1.0286,0.43198 -1.32617,0.87305c-0.28205,0.41807 -1.4175,1.75835 -1.76367,2.15234c-0.0046,-0.0028 0.02544,0.01104 -0.11133,-0.05664c-0.42813,-0.21189 -0.95173,-0.39205 -1.72656,-0.80078c-0.77483,-0.40873 -1.74407,-1.01229 -2.80469,-1.94727v-0.00195c-1.57861,-1.38975 -2.68437,-3.1346 -3.0332,-3.7207c0.0235,-0.02796 -0.00279,0.0059 0.04687,-0.04297l0.00195,-0.00195c0.35652,-0.35115 0.67247,-0.77056 0.93945,-1.07812c0.37854,-0.43609 0.54559,-0.82052 0.72656,-1.17969c0.36067,-0.71583 0.15985,-1.50352 -0.04883,-1.91797v-0.00195c0.01441,0.02867 -0.11288,-0.25219 -0.25,-0.57617c-0.13751,-0.32491 -0.31279,-0.74613 -0.5,-1.19531c-0.37442,-0.89836 -0.79243,-1.90595 -1.04102,-2.49609v-0.00195c-0.29285,-0.69513 -0.68904,-1.1959 -1.20703,-1.4375c-0.51799,-0.2416 -0.97563,-0.17291 -0.99414,-0.17383h-0.00195c-0.36964,-0.01705 -0.77527,-0.02148 -1.17773,-0.02148zM16.64258,15c0.38554,0 0.76564,0.0047 1.08398,0.01953c0.32749,0.01632 0.30712,0.01766 0.24414,-0.01172c-0.06399,-0.02984 0.02283,-0.03953 0.20898,0.40234c0.24341,0.57785 0.66348,1.58909 1.03906,2.49023c0.18779,0.45057 0.36354,0.87343 0.50391,1.20508c0.14036,0.33165 0.21642,0.51683 0.30469,0.69336v0.00195l0.00195,0.00195c0.08654,0.17075 0.07889,0.06143 0.04883,0.12109c-0.21103,0.41883 -0.23966,0.52166 -0.45312,0.76758c-0.32502,0.37443 -0.65655,0.792 -0.83203,0.96484c-0.15353,0.15082 -0.43055,0.38578 -0.60352,0.8457c-0.17323,0.46063 -0.09238,1.09262 0.18555,1.56445c0.37003,0.62819 1.58941,2.6129 3.48438,4.28125c1.19338,1.05202 2.30519,1.74828 3.19336,2.2168c0.88817,0.46852 1.61157,0.74215 1.77344,0.82227c0.38438,0.19023 0.80448,0.33795 1.29297,0.2793c0.48849,-0.05865 0.90964,-0.35504 1.17773,-0.6582l0.00195,-0.00195c0.3568,-0.40451 1.41702,-1.61513 1.92578,-2.36133c0.02156,0.0076 0.0145,0.0017 0.18359,0.0625v0.00195h0.00195c0.0772,0.02749 1.04413,0.46028 1.90625,0.87109c0.86212,0.41081 1.73716,0.8378 2.02148,0.97852c0.41033,0.20308 0.60422,0.33529 0.6543,0.33594c0.00338,0.08798 0.0068,0.18333 -0.00586,0.32813c-0.03507,0.40164 -0.14243,0.95757 -0.35742,1.55273c-0.10532,0.29136 -0.65389,0.89227 -1.3457,1.33008c-0.69181,0.43781 -1.53386,0.74705 -1.8457,0.79297c-0.9376,0.13815 -2.05083,0.18859 -3.27344,-0.19531c-0.84773,-0.26609 -1.90476,-0.61053 -3.27344,-1.19336c-2.77581,-1.18381 -5.13503,-3.19825 -6.82031,-4.97266c-0.84264,-0.8872 -1.51775,-1.71309 -1.99805,-2.33789c-0.4794,-0.62364 -0.68874,-0.94816 -0.86328,-1.17773l-0.00195,-0.00195c-0.30983,-0.40973 -2.20703,-3.04868 -2.20703,-5.42578c0,-2.51576 1.1685,-3.50231 1.80078,-4.18359c0.33194,-0.35766 0.69484,-0.41016 0.8418,-0.41016z"
                            ></path>
                          </g>
                        </g>
                      </svg>
                    </div>
                    <input
                      v-model="profile.no_hp"
                      type="tel"
                      placeholder="Masukkan nomor WhatsApp Anda"
                      class="w-full bg-gray-white rounded-xl pl-12 py-2 px-4 text-m text-green-950 placeholder-gray-500 focus:outline-none focus:bg-gradient-border border-[1.5px] border-gray-500"
                      :class="{
                        'border-red-400 focus:border-red-400 focus:ring-red-400/20':
                          errors.no_hp,
                      }"
                    />
                  </div>
                  <p v-if="errors.no_hp" class="text-red-500 text-sm md:font-medium">
                    {{ errors.no_hp }}
                  </p>
                </div>

                <!-- Password -->
                <div class="space-y-1">
                  <label
                    class="flex items-center text-gray-800 font-semibold text-[1rem]"
                  >
                    Password
                  </label>
                  <div class="relative">
                    <div class="absolute left-4 top-1/2 transform -translate-y-1/2">
                      <Lock class="md:w-4.5 md:h-4.5 w-4 h-4 text-[#16423C]" />
                    </div>
                    <input
                      v-model="profile.password"
                      :type="showPassword ? 'text' : 'password'"
                      placeholder="Isi jika ingin memperbarui password"
                      class="w-full bg-gray-white rounded-xl pl-12 py-2 px-4 text-m text-green-950 placeholder-gray-500 focus:outline-none focus:bg-gradient-border border-[1.5px] border-gray-500"
                      :class="{
                        'border-red-400 focus:border-red-400 focus:ring-red-400/20':
                          errors.password,
                      }"
                    />
                    <button
                      type="button"
                      @click="showPassword = !showPassword"
                      class="absolute right-5 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700 transition-colors duration-300"
                    >
                      <Eye v-if="showPassword" class="w-4 h-4" />
                      <EyeOff v-else class="w-4 h-4" />
                    </button>
                  </div>
                  <p v-if="errors.password" class="text-red-500 text-sm md:font-medium">
                    {{ errors.password }}
                  </p>
                </div>
              </div>
            </div>

            <!-- Tombol Aksi -->
            <div
              class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-12 pt-3"
            >
              <button
                type="submit"
                :disabled="isLoading"
                class="flex-1 relative group overflow-hidden bg-gradient-to-r from-green-600 to-blue-600 hover:from-green-500 hover:to-blue-500 text-white font-semibold md:py-3 py-2.5 px-8 md:rounded-2xl rounded-xl transition-all duration-500 transform hover:scale-101 disabled:opacity-50 disabled:cursor-not-allowed shadow-2xl hover:shadow-blue-500/25 uppercase"
              >
                <span
                  v-if="!isLoading"
                  class="flex items-center justify-center space-x-3 text-md"
                >
                  <Save class="w-5 h-5" />
                  <span>Simpan Pembaruan</span>
                </span>
                <span v-else class="flex items-center justify-center space-x-3 text-md">
                  <div
                    class="w-5 h-5 border-3 border-white border-t-transparent rounded-full animate-spin"
                  ></div>
                  <span>PEMROSESAN...</span>
                </span>

                <!-- Efek kilau tombol -->
                <div
                  class="absolute inset-0 bg-gradient-to-r from-transparent via-white/20 to-transparent transform -skew-x-12 -translate-x-full group-hover:translate-x-full transition-transform duration-1000"
                ></div>
              </button>

              <button
                type="button"
                @click="resetForm"
                class="flex-1 bg-white/5 hover:bg-gray-100 border border-red-800 hover:border-red-800 text-red-800 font-semibold md:py-3 py-2.5 px-8 md:rounded-2xl rounded-xl transition-all duration-300 backdrop-blur-sm flex items-center justify-center space-x-2 uppercase text-md"
              >
                <RotateCcw class="w-5 h-5" />
                <span>Reset</span>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>

    <!-- SweetAlert2 success notification (tidak perlu manual; Swal.fire() dipanggil di script) -->

    <!-- Scanning line effect -->
    <div
      class="absolute bottom-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-blue-500 to-transparent animate-pulse"
    ></div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from "vue";
import axios from "axios";
import Swal from "sweetalert2";
import "sweetalert2/dist/sweetalert2.min.css"; // pastikan CSS SweetAlert2 ter-include

// Icon‐icon dari lucide‐vue‐next
import {
  User,
  UserCheck,
  Mail,
  Phone,
  Lock,
  Camera,
  Edit,
  Eye,
  EyeOff,
  Save,
  RotateCcw,
  CheckCircle,
  MapPinHouseIcon,
} from "lucide-vue-next";

// ============================================
// 1. Konfigurasi Base URL dan Endpoints API
// ============================================
const API_BASE = import.meta.env.VITE_API_URL;
// Ganti dengan domain & prefix yang sesuai milikmu

// Endpoint untuk fetch data form (JSON)
const ENDPOINT_FETCH_FORM = `${API_BASE}/me`; // contoh: GET https://example.com/api/user/profile
// Endpoint untuk fetch gambar profil
const ENDPOINT_FETCH_IMAGE = `${API_BASE}/my-avatar`; // contoh: GET https://example.com/api/user/profile/image
// Endpoint untuk update data profile (JSON)
const ENDPOINT_UPDATE_PROFILE = `${API_BASE}/update-profile-user`; // contoh: PUT atau POST https://example.com/api/user/profile

// ============================================
// 2. Reactive State & Ref
// ============================================
const profileImageUrl = ref(null); // URL gambar profil yang di‐fetch dari server
const selectedImageFile = ref(null); // File gambar yang dipilih user (File object)
const showPassword = ref(false);
const isLoading = ref(false);
const fileInput = ref(null);

const token = localStorage.getItem("token");
const emit = defineEmits(["profile-updated"]);

const profile = reactive({
  name: "",
  email: "",
  no_hp: "",
  alamat: "",
  password: "",
});

const originalProfile = reactive({
  name: "",
  email: "",
  no_hp: "",
  alamat: "",
  // password biasanya tidak difetch dari server; field ini dipakai jika user ingin mengubah
  password: "",
});

const errors = reactive({
  name: "",
  email: "",
  no_hp: "",
  alamat: "",
  password: "",
});

// ============================================
// 3. Fungsi Utility: Validasi Form
// ============================================
const validateForm = () => {
  // Reset errors
  Object.keys(errors).forEach((key) => (errors[key] = ""));
  let isValid = true;

  if (!profile.name.trim()) {
    errors.name = "Nama lengkap wajib diisi";
    isValid = false;
  }

  // Validasi email
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(profile.email)) {
    errors.email = "Harap masukkan alamat email yang valid";
    isValid = false;
  }

  return isValid;
};

// ============================================
// 4. Fungsi Fetch Data Awal (GET Form + GET Image)
// ============================================
const fetchProfileData = async () => {
  try {
    // 4.1. GET data profil (JSON)
    const resForm = await axios.get(ENDPOINT_FETCH_FORM, {
      method: "GET",
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });

    const dataForm = resForm.data.data;
    profile.name = dataForm.name || "";
    profile.email = dataForm.email || "";
    profile.no_hp = dataForm.no_hp || "";
    profile.alamat = dataForm.alamat || "";
    profile.password = ""; // kosongkan, user harus mengetik baru jika ingin ganti

    originalProfile.name = dataForm.name || "";
    originalProfile.email = dataForm.email || "";
    originalProfile.no_hp = dataForm.no_hp || "";
    originalProfile.alamat = dataForm.alamat || "";
    originalProfile.password = "";

    // 4.2. GET gambar profil (mungkin berupa URL langsung)
    profileImageUrl.value = `${ENDPOINT_FETCH_IMAGE}/${dataForm.avatar}`;
  } catch (err) {
    console.error("Gagal fetch data profil:", err);
    await Swal.fire({
      icon: "error",
      title: "Gagal Memuat Data",
      text: "Tidak dapat mengambil data profil dari server. Coba refresh halaman.",
    });
  }
};

// Panggil fetch saat komponen mounted
onMounted(() => {
  fetchProfileData();
});

// ============================================
// 5. Fungsi Upload Gambar (jika user memilih file baru)
// ============================================
const triggerImageUpload = () => {
  fileInput.value?.click();
};

const handleImageUpload = (event) => {
  const file = event.target.files[0];
  if (!file) return;

  // Simpan File object untuk nanti di‐upload
  selectedImageFile.value = file;

  // Preview segera (sebagai data URL) agar user tahu gambarnya
  const reader = new FileReader();
  reader.onload = (e) => {
    profileImageUrl.value = e.target.result;
  };
  reader.readAsDataURL(file);
};

// ============================================
// 6. Fungsi Update (Upload Image, kemudian Update Profile)
// ============================================
const saveProfile = async () => {
  if (!validateForm()) return;

  isLoading.value = true;

  try {
    const formData = new FormData();
    formData.append("name", profile.name);
    formData.append("email", profile.email);
    formData.append("no_hp", profile.no_hp);
    formData.append("alamat", profile.alamat);
    if (profile.password) {
      formData.append("password", profile.password);
    }
    if (selectedImageFile.value) {
      formData.append("file", selectedImageFile.value);
    }

    const res = await axios.post(ENDPOINT_UPDATE_PROFILE, formData, {
      headers: {
        "Content-Type": "multipart/form-data",
        Authorization: `Bearer ${token}`,
      },
    });

    if (res.status === 200 && res.data.status === 200) {
      const updatedUser = res.data.data;

      originalProfile.name = updatedUser.name;
      originalProfile.email = updatedUser.email;
      originalProfile.no_hp = updatedUser.no_hp;
      originalProfile.alamat = updatedUser.alamat;
      originalProfile.password = "";

      selectedImageFile.value = null;

      if (updatedUser.avatar) {
        const newAvatarUrl = `${ENDPOINT_FETCH_IMAGE}/${updatedUser.avatar}`;
        profileImageUrl.value = newAvatarUrl;
        localStorage.setItem("avatarUrl", newAvatarUrl);
      }

      // ✅ Perbaikan di sini
      window.dispatchEvent(
        new CustomEvent("profile-updated", {
          detail: updatedUser,
        })
      );

      await Swal.fire({
        icon: "success",
        title: "Berhasil",
        text: "Profil berhasil diperbarui!",
        timer: 2000,
        showConfirmButton: false,
      });
    } else {
      await Swal.fire({
        icon: "warning",
        title: "Perhatian",
        text: `Server merespon: ${res.data.messages || res.status}`,
      });
    }
  } catch (err) {
    console.error("Error menyimpan profil:", err);
    let pesan = "Terjadi kesalahan saat menyimpan data.";
    if (err.response?.data?.message) {
      pesan = err.response.data.message;
    }
    await Swal.fire({
      icon: "error",
      title: "Gagal",
      text: pesan,
    });
  } finally {
    isLoading.value = false;
  }
};

// ============================================
// 7. Fungsi Reset Form ke Data Asli
// ============================================
const resetForm = () => {
  profile.name = originalProfile.name;
  profile.email = originalProfile.email;
  profile.no_hp = originalProfile.no_hp;
  profile.alamat = originalProfile.alamat;
  profile.password = originalProfile.password;
  Object.keys(errors).forEach((key) => (errors[key] = ""));
  // Kembalikan gambar ke versi yang terakhir di fetch dari server
  fetchProfileImageOnly();
};

// Fungsi khusus ambil ulang gambar saja (dipakai untuk reset)
const fetchProfileImageOnly = async () => {
  try {
    const resImg = await axios.get(ENDPOINT_FETCH_IMAGE, {
      responseType: "json",
    });
    if (resImg.data && resImg.data.imageUrl) {
      profileImageUrl.value = resImg.data.imageUrl;
    } else {
      profileImageUrl.value = null;
    }
  } catch (err) {
    console.error("Gagal fetch gambar profil:", err);
    profileImageUrl.value = null;
  }
};
</script>

<style scoped>
/* Kelas kustom untuk gradient border pada focus */
.focus\:bg-gradient-border:focus {
  /* Border jadi transparent */
  border-color: transparent !important;
  /* Dua lapis background:
    - lapis atas putih untuk isi input
    - lapis bawah gradient untuk border */
  background-image: linear-gradient(white, white),
    linear-gradient(to right, #16a34a, #3b82f6);
  /* Atur origin & clip supaya:
    - lapis putih hanya di padding-box (isi)
    - gradient hanya di border-box */
  background-origin: padding-box, border-box;
  background-clip: padding-box, border-box;
}
/* Animasi & styling scroll yang sudah ada */
@keyframes float {
  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
  }
}

@keyframes float-delayed {
  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-15px) rotate(-180deg);
  }
}

@keyframes float-slow {
  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-10px) rotate(90deg);
  }
}

@keyframes scan {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(400%);
  }
}

.animate-float {
  animation: float 6s ease-in-out infinite;
}

.animate-float-delayed {
  animation: float-delayed 8s ease-in-out infinite;
}

.animate-float-slow {
  animation: float-slow 10s ease-in-out infinite;
}

.animate-scan {
  animation: scan 3s linear infinite;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 12px;
}

::-webkit-scrollbar-track {
  background: #f1f5f9;
  border-radius: 6px;
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(to bottom, #3b82f6, #8b5cf6);
  border-radius: 6px;
}

::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(to bottom, #2563eb, #7c3aed);
}
</style>
