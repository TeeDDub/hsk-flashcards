<template>
  <div class="home-container w-full flex flex-col h-screen">
    <div class="w-full flex-grow flex items-center">
      <div class="w-1/2 h-1/2 md:w-full mx-auto">
        <div class="w-full">
          <select v-model="level">
          <option v-for="i in 6" :key="i" :value="i">HSK {{ i }}급</option>
          </select>
          <p>No.{{ currentId[level] }}</p>
        </div>
        <div class="flex w-full">
          <button @click="prev" class="basis-1/12" id="prev" style="background-color: #ccc; border: none; border-radius: 5px; color: #fff;">⏪️</button>
          <FlashCard class="basis-10/12" style="border: none; border-radius: 5px;"
            :entry="data[currentId[level]].entry" :parts="data[currentId[level]].parts" :pron="data[currentId[level]].pron" :means="data[currentId[level]].means" />
          <button @click="next" class="basis-1/12" id="next" style="background-color: #ccc; border: none; border-radius: 5px; color: #fff;">⏩️</button>
        </div>
      </div>
    </div>
    <div class="h-100px">
      <p class="text-gray-400 text-center">
        <ul>
          <li>만든 사람: <a href="https://github.com/TeeDDub">@TeeDDub</a></li>
          <li>도움주신 분: <a href="https://github.com/malkoG">@malkoG</a></li>
        </ul>
      </p>
    </div>
  </div>
</template>

<script>
import FlashCard from './FlashCard.vue'

export default {
  name: 'HomeContainer',
  props: {
    msg: String
  },
  components: {
    FlashCard
  },
  data() {
    return {
      level: null,
      currentId: null,
      data: null,
    }
  },
  methods: {
    prev() {
      if (this.currentId[this.level] > 1) {
        this.currentId[this.level]--;
      } else {
        this.currentId[this.level] = Object.keys(this.data).length;

      }
      localStorage.setItem('currentId', JSON.stringify(this.currentId));
    },
    next() {
      if (this.currentId[this.level] < Object.keys(this.data).length) {
        this.currentId[this.level]++;
      } else {
        this.currentId[this.level] = 1;
      }
      localStorage.setItem('currentId', JSON.stringify(this.currentId));
    }
  },
  watch: {
    level(newLevel) {
      localStorage.setItem('level', newLevel);
      this.data = require(`@/assets/data/hsk${newLevel}.json`);
    }
  },
  created() {
    this.level = localStorage.getItem('level')
    const storedCurrentId = localStorage.getItem('currentId');
    this.currentId = storedCurrentId ? JSON.parse(storedCurrentId) : {1: 1, 2: 1, 3: 1, 4: 1, 5: 1, 6: 1};

    if(this.level === null) {
      this.level = 1
      localStorage.setItem('level', this.level)
    }
    if(storedCurrentId === null) {
      localStorage.setItem('currentId', JSON.stringify(this.currentId));
    }
    this.data = require(`@/assets/data/hsk${this.level}.json`);
  }
}
</script>
