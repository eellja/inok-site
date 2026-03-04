<script setup>
import { ref } from 'vue'

const activeTab = ref('журнал')
const isMobileMenuOpen = ref(false)

const tabs = [
  { id: 'журнал', label: 'Журнал' },
  { id: 'про нас', label: 'Про нас' },
  { id: 'публікуватись', label: 'Хочу публікуватись' },
  { id: 'підтримка', label: 'Підтримка' }
]

const switchTab = (tabId) => {
  activeTab.value = tabId
  isMobileMenuOpen.value = false
}
</script>

<template>
  <div 
    class="min-h-screen bg-blue-950 bg-cover bg-no-repeat bg-fixed bg-center md:p-8 text-blue-900 font-serif flex flex-col transition-all duration-300 relative overflow-hidden"
    style="background-image: url('/background.jpg');"
  >
    <div class="absolute inset-0 bg-black/60 z-0"></div>
    
    <div class="z-10 flex-1 flex flex-col w-full max-w-7xl mx-auto bg-white md:border-2 md:border-blue-900 p-4 md:p-10 md:shadow-[8px_8px_0px_rgba(30,58,138,1)] transition-all duration-300">

      <header :class="[
        'flex items-center justify-between transition-all duration-300 z-20',
        isMobileMenuOpen 
          ? 'pb-4 lg:pb-5 lg:border-b-2 lg:border-blue-900 lg:mb-8' 
          : 'pb-5 border-b-2 border-blue-900 mb-8'
      ]">
        <div class="font-bold text-2xl md:text-3xl tracking-widest text-red-600 uppercase shrink-0 transition-all duration-300">Інок</div>
        
        <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="lg:hidden text-blue-900 focus:outline-none ml-4 transition-transform duration-300 hover:scale-110">
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="isMobileMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"></path>
          </svg>
        </button>

        <nav class="hidden lg:flex items-center gap-2">
          <button 
            v-for="tab in tabs" 
            :key="tab.id" 
            @click="switchTab(tab.id)"
            :class="[
              'border rounded-full px-5 py-1 text-sm uppercase tracking-wide transition-all duration-300 whitespace-nowrap',
              activeTab === tab.id 
                ? (tab.id === 'публікуватись' ? 'bg-red-600 text-white border-red-600 shadow-[2px_2px_0px_rgba(220,38,38,1)]' : 'bg-blue-900 text-white border-blue-900 shadow-[2px_2px_0px_rgba(30,58,138,1)]') 
                : (tab.id === 'публікуватись' ? 'border-red-600 text-red-600 hover:bg-red-600 hover:text-white' : 'border-blue-900 text-blue-900 hover:bg-blue-900 hover:text-white')
            ]"
          >
            {{ tab.label }}
          </button>
        </nav>
      </header>

      <nav v-if="isMobileMenuOpen" class="lg:hidden flex flex-col gap-3 mb-8 border-b-2 border-blue-900 pb-6 animate-fade-in transition-all duration-300">
        <button 
          v-for="tab in tabs" 
          :key="tab.id" 
          @click="switchTab(tab.id)"
          :class="[
            'border rounded-full px-5 py-3 text-sm uppercase tracking-wide transition-colors text-center',
            activeTab === tab.id 
              ? (tab.id === 'публікуватись' ? 'bg-red-600 text-white border-red-600' : 'bg-blue-900 text-white border-blue-900') 
              : (tab.id === 'публікуватись' ? 'border-red-600 text-red-600' : 'border-blue-900 text-blue-900')
          ]"
        >
          {{ tab.label }}
        </button>
      </nav>

      <main class="flex-1 flex flex-col transition-all duration-300">
        
        <div v-if="activeTab === 'журнал'" class="animate-fade-in transition-all duration-300">
          <h1 class="text-2xl md:text-3xl font-bold mb-8 text-blue-900 tracking-wider">Випуски журналів</h1>
          
          <div class="flex items-center gap-6">
            <a href="/inok-issue-1.pdf" target="_blank" class="shrink-0 w-32 h-32 md:w-40 md:h-40 border-2 border-red-600 flex items-center justify-center text-4xl font-bold text-red-600 hover:bg-red-600 hover:text-white transition-all duration-300 hover:-translate-y-1 hover:shadow-[4px_4px_0px_rgba(220,38,38,1)]">
              №1
            </a>
            <span class="text-xl md:text-2xl text-blue-900 italic opacity-70">Далі буде...</span>
          </div>
        </div>

        <div v-else-if="activeTab === 'про нас'" class="max-w-2xl animate-fade-in transition-all duration-300">
          <h2 class="text-2xl md:text-3xl font-bold mb-6 text-blue-900 transition-all duration-300">Про нас</h2>
          
          <p class="text-lg md:text-xl italic text-blue-900 leading-relaxed mb-6 border-l-4 border-red-600 pl-4 transition-all duration-300">
            Ми студ. ініціатива Могилянки, художньо-публіцистичний вісник з філософсько-релігієзнавчим нахилом. Шукаємо тексти.
          </p>

          <p class="text-lg leading-relaxed mb-4 transition-all duration-300">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quis animi nisi, magni temporibus asperiores reprehenderit reiciendis unde quia aliquam, magnam vel! Impedit voluptate totam consequuntur ullam vitae tenetur, alias beatae? 
          </p>
        </div>

        <div v-else-if="activeTab === 'публікуватись'" class="max-w-2xl animate-fade-in transition-all duration-300">
          <h2 class="text-2xl md:text-3xl font-bold mb-6 text-red-600 transition-all duration-300">Шукаємо тексти</h2>
          <p class="text-lg leading-relaxed mb-4 transition-all duration-300">
            Вимоги до текстів <br> <a href="#" class="text-blue-900 underline">Форма</a> для надсилання рукописів.
          </p>
        </div>

        <div v-else-if="activeTab === 'підтримка'" class="max-w-2xl animate-fade-in transition-all duration-300">
          <h2 class="text-2xl md:text-3xl font-bold mb-6 text-blue-900 transition-all duration-300">Підтримка проєкту</h2>
          <p class="text-lg leading-relaxed mb-4 transition-all duration-300">
            Інформація про те, як можна підтримати ваш самвидав: посилання на банку або інші реквізити.
          </p>
        </div>

      </main>
    </div>
  </div>
</template>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.3s ease-in-out;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(5px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>