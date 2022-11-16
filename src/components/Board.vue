<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem v-for="field in fields" :field="field" :game-status="gameStatus" :key="field.id" @selectField="selectField($event)"/>
    </div>
    <div>
      <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>
    </div>
    <div>
      <button class="btn" @click="start" :disabled="!canStartGame">Старт</button>
    </div>
    <div>
      <p class="win" v-if="isWin">Поздравляем! Вас ждёт следующий раунд.</p>
      <p class="fail" v-if="isFail">Поражение! Попробуйте снова...</p>
    </div>
  </div>
</template>

<script>
import BoardItem from './BoardItem.vue';
import useGameInit from "./composables/useGameInit";
import useGameStart from "./composables/useGameStart";
import { ref } from 'vue';
import {GAME_STATUS} from "../constants";
import useGameProcess from "./composables/useGameProcess";

export default {
  name: 'Board',
  components: {
    BoardItem
  },
  setup() {
    const number = 25;
    const gameStatus = ref(GAME_STATUS.NONE);

    const { difficult, fields, init} = useGameInit(number);
    const { start, canStartGame } = useGameStart(init, fields, difficult, number, gameStatus);
    const { selectField, isWin, isFail } = useGameProcess(fields, gameStatus, difficult, start);

    return { difficult, fields, init, number, start, gameStatus, canStartGame, selectField, isFail, isWin};
  },
}

</script>

<style scoped>
.board-wrapper {
  margin-bottom: 40px;
}
.board {
  width: 300px;
  background-color: #eee;
  margin: 0 auto;
}

.btn {
  background: #42b983cc;
  color: white;
  border: none;
  border-radius: 2px;
  padding: 10px 30px;
  margin: 10px 0;
  cursor: pointer;
  outline: none;
}

.btn:hover {
  background: #42b983;
}

.btn:disabled {
  opacity: 0.5;
}

.win {
  color: #42b983;
}

.fail {
  color: #ff000055;
}

</style>