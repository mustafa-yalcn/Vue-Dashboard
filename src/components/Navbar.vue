<template>
  <header class="sticky top-0 z-10 bg-white dark:bg-backgroundDark dark:border-b dark:border-primary/10 shadow-sm px-4 py-2 flex items-center justify-between">
    <nav class="lg:hidden">
      <button @click="$emit('toggle-drawer')" class="btn btn-square btn-ghost">
        <component :is="getIcon('Bars3Icon')" class="w-6 h-6 text-gray-700 dark:text-white" />
      </button>
    </nav>
    <section class="flex-1 mx-4">
      <div class="relative max-w-md mx-auto">
        <input
          type="text"
          placeholder="Search"
          class="input input-bordered w-full rounded-full px-4 py-2 dark:bg-white/5 dark:backdrop-blur-md dark:border-white/10"
        />
      </div>
    </section>
    <section class="flex items-center gap-4">
      <button
        @click="$emit('toggle-theme')"
        class="btn btn-ghost btn-circle dark:bg-white/5 dark:backdrop-blur-md dark:border-white/10"
      >
        <component
          :is="getIcon(isDark ? 'MoonIcon' : 'SunIcon')"
          class="w-6 h-6 text-gray-800 dark:text-white"
        />
      </button>
      <div class="dropdown dropdown-end">
       <button tabindex="0" class="btn btn-ghost btn-circle avatar">
    <span
      class="w-10 h-10 rounded-full overflow-hidden border dark:border-white/10 flex items-center justify-center bg-white dark:bg-gray-800"
    >
      <UserIcon class="w-6 h-6 text-gray-600 dark:text-gray-300" />
    </span>
  </button>
        <ul
          tabindex="0"
          class="mt-3 p-2 shadow menu menu-sm dropdown-content bg-base-100 dark:bg-backgroundDark rounded-box w-48 text-sm font-medium space-y-1"
        >
          <li><a>Profil</a></li>
          <li><a>Ayarlar</a></li>
          <li><a>Çıkış</a></li>
        </ul>
      </div>
    </section>
  </header>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
import * as HeroIcons from '@heroicons/vue/24/outline'
import { UserIcon } from '@heroicons/vue/24/outline'
defineProps({
  isDark: {
    type: Boolean,
    required: true,
  },
})

defineEmits(['toggle-drawer', 'toggle-theme'])

const getIcon = (name) => HeroIcons[name] || null
</script>