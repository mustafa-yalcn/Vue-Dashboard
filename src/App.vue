<template>
  <div class="drawer lg:drawer-open font-display">
    <input type="checkbox" id="my-drawer" class="drawer-toggle" >
 <div class="drawer-content flex flex-col  bg-white dark:bg-backgroundDark">
  <Navbar :isDark="isDark" @toggle-drawer="toggleDrawer" @toggle-theme="toggleTheme" />
 <main class="flex-1 p-6 bg-white dark:bg-backgroundDark">
  <StatsCard />
  <div class="grid grid-cols-1 gap-6 mb-6">
<Carts/>
<div class="grid grid-cols-1 lg:grid-cols-3 gap-6"> 
  <RecentOrders class="lg:col-span-2" />
  <RecentActivity/>
</div>
<stackedBarChart />
  </div>
 </main>
</div>
 
 <Sidebar />
 </div>
</template>
<script setup>
import { onMounted,ref, watchEffect } from 'vue';
import Navbar from './components/Navbar.vue';
import Sidebar from './components/Sidebar.vue';
import StatsCard from './components/StatsCards.vue';
import Carts from './components/Carts.vue';
import RecentOrders from './components/RecentOrders.vue';
import RecentActivity from './components/RecentActivity.vue';
import stackedBarChart from './components/StackedBarChart.vue';
const isDark=ref(true);

onMounted(()=>{
  const savedTheme =localStorage.getItem('theme');
  const systemPrefersDark=window.matchMedia("(prefers-color-scheme:dark)").matches;
  if(savedTheme){
    isDark.value=savedTheme==='dark';
  }
  else if(systemPrefersDark){
    isDark.value=true
  }
});
watchEffect(()=>{
  const html=document.documentElement;
  if(isDark.value){
    html.setAttribute('data-theme','dark');
    localStorage.setItem('theme','dark')
  }else{
    html.setAttribute('data-theme','light');
    localStorage.setItem('theme','light')
  }
})
const toggleTheme=()=>{
  isDark.value=!isDark.value;
};
const toggleDrawer = () =>{
  const drawer =document.getElementById('my-drawer');
  if(drawer){
    drawer.checked=!drawer.checked
  }
}
</script>
