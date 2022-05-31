<template>
    <div @click="$emit('click')" class="square">
      <span class="game-piece" :class="value" v-if="value !== ''">{{ value }}</span>
    </div>
</template>

<style>
.square {
    width: 64px;
    height: 64px;
    border: 2px solid rgb(255, 255, 255);
    font-size: 42px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.game-piece {
    text-transform: uppercase;
}
.x {
    color: #ffc6ff;
}
.o {
    color: #caffbf;
}
</style>

<script>
  export default {
    props: {
      value: String,
    }
  }
</script>
