<template>
  <div class="test-form my-[100px]">
      <div class="container">
          <div class="flex flex-col justify-center items-center">
                <div class="justify-center shadow-lg border-gray-300 border-2 p-[20px] w-3/5 bg-blue-50 rounded-3xl">
                    <div class="my-3">
                      <p class="font-bold">Результат теста "Шахматы" <br> пользователя Павел</p>
                  </div>
                </div>

            <div v-for="question in activeUserResult.questions" :key="question.number" class="justify-center my-8 items-stretch shadow-lg border-gray-300 border-2 p-[20px] w-3/5 bg-blue-50 rounded-3xl">
              <div class="my-3">
                <p class="font-bold">Вопрос {{ question.number + 1 }}</p>
              </div>
              <hr>
              <div class="flex justify-start my-3">
                <p class="font-medium">{{question.question_text}}</p>
              </div>
              <div class="justify-start">
                <div v-for="answer in question.answers" :key="answer.number" class="flex my-3 items-center">
                  <div v-if="question.answer.includes(answer.number)" class="w-4 h-4 border border-gray-300 rounded bg-blue-700 focus:ring-3 focus:ring-blue-300 dark:bg-gray-600 dark:border-gray-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800"></div>
                  <div v-if="!question.answer.includes(answer.number)" class="flex w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-600 dark:border-gray-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800"></div>
                  <p class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">{{ answer.title }}</p>
                </div>
              </div>
            </div>

<!--            TODO логику для психологических тестов и тд ( мб коммент вне зависимости от ответа)-->
                <div class="justify-center shadow-lg my-3 border-gray-300 border-2 p-[20px] w-3/5 bg-blue-50 rounded-3xl">
                     
                    <!-- отображать 2 блока ниже если тест с типом Phiho: -->
                    
                     <div v-if="activeUserResult.type == 'Psiho'" class="my-3">
                        <p class="font-bold">Итоговый результат</p>
                    </div>
                    <hr>
                    
                    <!-- форма для ответа:  -->
                    <div v-if="activeUserResult.type == 'Psiho'" class="flex justify-start my-3">
                      <p class="font-medium">ВСТАВИТЬ РЕЗУЛЬТАТ</p> 
                    </div>
                  




                    
                    <div class="my-3">
                        <p class="font-bold">Оставить комментарий</p>
                    </div>
                    <hr>
                    
                    <div class="flex flex-col my-3 items-center">
                        <input
                            :value="activeUserResult.comment"
                            @input="event => this.$store.commit('addAnswerForAR' ,event.target.value)"
                            type="text" class="w-full rounded-lg bg-gray-50 border border-gray-300 text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                    </div>

                    <div class="flex justify-center my-3">
                        <button @click="addComment" class="text-white mx-10 bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" type="button">
                            <p class="p-2 font-bold">Подтвердить</p>
                        </button>
                    </div>
                    
                </div>
          </div>
      </div>
  </div>

</template>

<script>
import {mapState} from "vuex";

export default {
  name: "test-form",
  computed: mapState({
    activeUserResult: state => state.creatorM.activeUserResult,
  }),
  methods:{
    addComment(){
      this.$store.dispatch('addComment')
      this.$router.push('/myowntests')
    }
  }
}
</script>

<style>

</style>