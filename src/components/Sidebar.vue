<template>
  <aside class="drawer-side dark:bg-backgroundDark border-r border-gray-200 dark:border-primary/10">
    <label for="my-drawer" aria-label="Close sidebar" class="drawer-overlay"></label>
    <nav class="menu p-4 w-80 min-h-full text-gray-800 dark:text-gray-200" aria-label="Main navigation">
      <header class="mb-4 mt-6 justify-center items-center flex ">
        <img src="../assets/images/logo4.PNG" class="mt-2 bg-backgroundLight dark:bg-backgroundDark">
      </header>
      <ul role="menu">
        <li role="none" class="p-2 text-lg" v-for="(link, index) in links" :key="index">
          <button
            role="menuitem"
            :aria-expanded="!!link.children && link.open"
            :aria-haspopup="!!link.children"
            :class="{ active: link.active }"
            @click="setActive(index)"
            class="flex items-center w-full text-left hover:bg-gray-100 dark:hover:bg-white/10 text-black dark:text-white"
          >
            <component :is="getIconComponent(link.icon)" class="w-5 h-5" />
            <span class="ml-2">{{ link.name }}</span>
            <span v-if="link.children" class="ml-auto dropdown-icon">
              <component
                :is="getIconComponent(link.open ? 'ChevronDownIcon' : 'ChevronRightIcon')"
                class="w-4 h-4"
              />
            </span>
          </button>
          <ul v-if="link.children && link.open" class="pl-8">
            <li v-for="(child, childIndex) in link.children" :key="childIndex">
              <a href="#" class="flex items-center py-1 gap-2 hover:bg-gray-100 dark:hover:bg-white/10 text-black dark:text-white">
                <component :is="getIconComponent(child.icon)" class="w-4 h-4" />
                {{ child.name }}
              </a>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </aside>
</template>
<script setup>
import * as HeroIcons from '@heroicons/vue/24/outline'
import { ref } from 'vue'

const getIconComponent = (name) => {
  return HeroIcons[name] || null
}

const links = ref([
  { name: 'Ana Sayfa', icon: 'HomeIcon', active: true, open: false },
  { name: 'Veriler', icon: 'ChartBarIcon', active: false, open: false },
  { name: 'Raporlar', icon: 'DocumentTextIcon', active: false, open: false },
  {
    name: 'Kullanıcılar',
    icon: 'UserIcon',
    active: false,
    open: false,
    children: [
      { name: 'Tüm Kullanıcılar', icon: 'UsersIcon' },
      { name: 'Yeni Kullanıcılar', icon: 'UserPlusIcon' }
    ]
  },
  {
    name: 'Ürünler',
    icon: 'ShoppingCartIcon',
    active: false,
    open: false,
    children: [
      { name: 'Tüm Ürünler', icon: 'TagIcon' },
      { name: 'Kategoriler', icon: 'TagIcon' }
    ]
  },
  { name: 'Mesajlar', icon: 'EnvelopeIcon', active: false, open: false },
  { name: 'Ayarlar', icon: 'Cog6ToothIcon', active: false, open: false }
])

const setActive = (index) => {
  if (links.value[index].children) {
    links.value[index].open = !links.value[index].open
  }
  links.value.forEach((link, i) => {
    link.active = i === index
  })
}
</script>