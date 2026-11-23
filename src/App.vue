<script setup>
import { ref } from 'vue'

const photoUrl = `${import.meta.env.BASE_URL}kot.jpg`

const step = ref(0)

const questions = [
  {
    subtitle: 'a little surprise for you',
    title: 'У меня кое-что есть для тебя',
    button: '🌷 Нажми меня',
    hint: 'Небольшой сюрприз ждёт тебя'
  },
  {
    subtitle: 'one little question',
    title: 'Ты точно уверена что хочешь увидеть что там?',
    button: 'Да',
    hint: 'Подумай хорошенько...'
  },
  {
    subtitle: 'are you really sure?',
    title: 'Прям точно-точно?',
    button: 'Наверное...',
    hint: 'Назад дороги нет...'
  },
  {
    subtitle: 'almost there',
    title: 'Ну ты прям уверена? Не боишься взломанного компьютера?',
    button: 'Да давай уже, показывай',
    hint: 'Осталось совсем чуть-чуть'
  }
]

function nextStep() {
  if (step.value < questions.length) {
    step.value++
  }
}

function restart() {
  step.value = 0
}
</script>

<template>
  <main class="page">
    <div class="card">
      <Transition name="fade" mode="out-in">

        <div v-if="step < questions.length" :key="step" class="question-content">
          <p class="subtitle">{{ questions[step].subtitle }}</p>

          <h1>{{ questions[step].title }}</h1>

          <button class="surprise-button" @click="nextStep">
            {{ questions[step].button }}
          </button>

          <p class="hint">{{ questions[step].hint }}</p>
        </div>

        <div v-else key="final" class="surprise-content">
          <img
            :src="photoUrl"
            alt="Котик с букетом"
            class="surprise-image"
          />

          <h1>Это для тебя!</h1>

          <p class="message">
            Мар, ты справишься с сессией, даже не сомневайся. Ты очень много работаешь и это самое главное, у тебя все получится, главное перебороть этот страх провала. А в этом тебе поможет котик с букетиком через интернетик!
          </p>

          <button class="surprise-button" @click="restart">
            Вернуться назад
          </button>
        </div>

      </Transition>
    </div>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
}

.page {
  min-height: 100vh;
  background-color: #fff0f5;

  display: flex;
  justify-content: center;
  align-items: center;

  padding: 20px;
}

.card {
  width: 100%;
  max-width: 500px;
  min-height: 310px;

  background-color: #fff9fc;
  border-radius: 24px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  padding: 30px;
  text-align: center;
}

.subtitle {
  color: #c47d9b;
  font-size: 13px;
}

h1 {
  color: #a75d80;
  font-size: 26px;
  margin: 15px 0 25px;
}

.surprise-button {
  background-color: #e9a9c3;
  color: #ffffff;

  border: none;
  border-radius: 25px;

  padding: 13px 28px;
  font-size: 16px;

  cursor: pointer;
  transition: 0.3s;
}

.surprise-button:hover {
  background-color: #d98aab;
  transform: scale(1.05);
}

.hint {
  margin-top: 25px;
  color: #b98ca0;
  font-size: 13px;
}
.surprise-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;

  animation: appear 0.7s ease;
}

.surprise-image {
  width: 100%;
  max-width: 280px;
  border-radius: 18px;
  object-fit: cover;
}

.message {
  color: #a75d80;
  font-size: 16px;
  line-height: 1.6;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(15px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.question-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.35s ease, transform 0.35s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
</style>