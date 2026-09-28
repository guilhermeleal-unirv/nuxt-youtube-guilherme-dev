<script setup lang="ts">
import { ref, reactive } from 'vue';

const form = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: [] as string[],
  mensagem: ''
});

const isSubmitting = ref(false);
const successMessage = ref('');

const cursos = [
  'Engenharia de Software',
  'Ciência da Computação',
  'Sistemas de Informação',
  'Design / UI/UX',
  'Outro'
];

const interessesOptions = [
  'Front-end',
  'Back-end',
  'Mobile',
  'UI/UX',
  'DevOps',
  'IA/Machine Learning'
];

const submitForm = () => {
  // Simular uma chamada de API
  isSubmitting.value = true;
  successMessage.value = '';
  
  setTimeout(() => {
    console.log('Formulário enviado com sucesso:', form);
    successMessage.value = 'Cadastro realizado com sucesso! Bem-vindo(a) ao time.';
    
    // Limpar o formulário reativamente
    form.nome = '';
    form.email = '';
    form.curso = '';
    form.semestre = '';
    form.interesses = [];
    form.mensagem = '';
    
    isSubmitting.value = false;
    
    // Remover mensagem de sucesso após 5 segundos
    setTimeout(() => {
      successMessage.value = '';
    }, 5000);
  }, 1000);
};
</script>

<template>
  <div class="min-h-screen bg-gray-50 flex flex-col justify-center py-12 sm:px-6 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-md">
      <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">
        Cadastro de Novo Membro
      </h2>
      <p class="mt-2 text-center text-sm text-gray-600">
        Junte-se à nossa comunidade preenchendo o formulário abaixo.
      </p>
    </div>

    <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-xl">
      <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10 border border-gray-200">
        
        <!-- Mensagem de Sucesso -->
        <div v-if="successMessage" class="mb-6 p-4 rounded-md bg-green-50 border border-green-200">
          <div class="flex">
            <div class="flex-shrink-0">
              <svg class="h-5 w-5 text-green-400" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
            </div>
            <div class="ml-3">
              <p class="text-sm font-medium text-green-800">{{ successMessage }}</p>
            </div>
          </div>
        </div>

        <form @submit.prevent="submitForm" class="space-y-6">
          
          <!-- Nome -->
          <div>
            <label for="nome" class="block text-sm font-medium text-gray-700">Nome completo <span class="text-red-500">*</span></label>
            <div class="mt-1">
              <input id="nome" v-model="form.nome" type="text" required placeholder="Ex: João da Silva"
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
            </div>
          </div>

          <!-- E-mail -->
          <div>
            <label for="email" class="block text-sm font-medium text-gray-700">E-mail <span class="text-red-500">*</span></label>
            <div class="mt-1">
              <input id="email" v-model="form.email" type="email" required placeholder="joao@exemplo.com"
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-6 sm:grid-cols-2 sm:gap-x-4">
            <!-- Curso -->
            <div>
              <label for="curso" class="block text-sm font-medium text-gray-700">Curso / Área</label>
              <div class="mt-1">
                <select id="curso" v-model="form.curso" class="block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md shadow-sm border">
                  <option value="" disabled>Selecione uma opção</option>
                  <option v-for="curso in cursos" :key="curso" :value="curso">{{ curso }}</option>
                </select>
              </div>
            </div>

            <!-- Semestre -->
            <div>
              <label for="semestre" class="block text-sm font-medium text-gray-700">Semestre / Período</label>
              <div class="mt-1">
                <input id="semestre" v-model="form.semestre" type="number" min="1" max="12" placeholder="Ex: 3"
                  class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
              </div>
            </div>
          </div>

          <!-- Interesses -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Interesses / Habilidades</label>
            <div class="grid grid-cols-2 gap-2 sm:grid-cols-3">
              <div v-for="interesse in interessesOptions" :key="interesse" class="flex items-center">
                <input :id="'interesse-' + interesse" v-model="form.interesses" :value="interesse" type="checkbox"
                  class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded" />
                <label :for="'interesse-' + interesse" class="ml-2 block text-sm text-gray-900">
                  {{ interesse }}
                </label>
              </div>
            </div>
          </div>

          <!-- Mensagem / Bio -->
          <div>
            <label for="mensagem" class="block text-sm font-medium text-gray-700">Mensagem / Bio curta</label>
            <div class="mt-1">
              <textarea id="mensagem" v-model="form.mensagem" rows="3" maxlength="300" placeholder="Conte-nos um pouco sobre você..."
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm"></textarea>
            </div>
            <p class="mt-2 text-sm text-gray-500 text-right">{{ form.mensagem.length }}/300</p>
          </div>

          <!-- Submit Button -->
          <div>
            <button type="submit" :disabled="isSubmitting"
              class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-colors duration-200 disabled:opacity-70 disabled:cursor-not-allowed">
              <span v-if="isSubmitting" class="flex items-center">
                <svg class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                Enviando...
              </span>
              <span v-else>Cadastrar</span>
            </button>
          </div>
          
        </form>
      </div>
      
      <div class="mt-4 text-center">
        <NuxtLink to="/" class="font-medium text-blue-600 hover:text-blue-500 text-sm">
          &larr; Voltar para a página inicial
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Estilos adicionais se necessário, a maioria é suprida pelo Tailwind */
</style>
