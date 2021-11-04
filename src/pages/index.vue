<template>
  <div class="container">
    <h1 class="title">いろいろな さんかくをつくる</h1>
    <div class="adjuster">
      <div class="adjuster-figure">
        <div
          ref="hoge"
          class="triangle"
          :class="adjusterClass"
          :style="{
            borderWidth: range + 'px'
          }"
        ></div>
        <!-- <div v-show="targetStyle">{{ targetStyle }}</div> -->
      </div>
      <input type="range" name="speed" class="adjuster-range" :value="range" min="1" max="100" step="1" @input="changeRange">
      <div class="adjuster-text">{{ range }}</div>
    </div>
    <ul class="figure_list">
      <li class="figure_list-item">
        <div class="triangle triangle--top" @click="updateAdjuster('top')"></div>
      </li>
      <li class="figure_list-item">
        <div class="triangle triangle--bottom" @click="updateAdjuster('bottom')"></div>
      </li>
      <li class="figure_list-item">
        <div class="triangle triangle--left" @click="updateAdjuster('left')"></div>
      </li>
      <li class="figure_list-item">
        <div class="triangle triangle--right" @click="updateAdjuster('right')"></div>
      </li>
    </ul>
    <!-- <div class="arrow"></div> -->
  </div>
</template>

<script lang="ts">
import {
  computed,
  defineComponent,
  onMounted,
  reactive,
  ref,
  watch
} from '@nuxtjs/composition-api'

export default defineComponent({
  setup(_, context) {
    const range = ref(30)
    // const targetStyle = reactive({})
    const adjusterClass = ref('triangle--top')
    const style = reactive({
      borderWidth: 0,
      borderStyle: 'solid',
      borderBottom: '#555',
      borderTop: '',
      borderLeft: 'transparent',
      borderRight: 'transparent',
    })

    // const targetStyle = computed(() => {
    //   return context.refs.hoge?.style.borderWidth || {}
    // })

    const changeRange = (value: { target: HTMLButtonElement }) => {
      range.value = Number(value.target.value)
      // targetStyle.value = {
      //   'border-top': range + 'px solid #555',
      //   'border-bottom': range + 'px solid #555',
      //   'border-left': range + 'px solid #555',
      //   'border-right': range + 'px solid #555',
      // }
    }

    const updateAdjuster = (type: string) => {
      adjusterClass.value = 'triangle--' + type
    }

    // const updateStyle = (type) => {

    // }

    // watch(
    //   targetStyle,
    //   () => {
    //     console.log(targetStyle.value)
    //   }
    // )

    // onMounted(() => {
    //   console.log(context.refs.hoge?.style)
    // })

    return {
      // targetStyle,
      adjusterClass,
      range,
      style,
      changeRange,
      updateAdjuster
    }
  },
})
</script>

<style lang="scss">
.container {
  padding: 30px;
  color: #555;
}

.title {
  text-align: center;
}

.adjuster {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-top: 50px;

  &-figure {
    // position: relative;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 200px;
    height: 200px;
  }

  &-range {
    margin-top: 50px;
    appearance: none;
    cursor: pointer;
    outline: none;
    height: 14px;
    width: 300px;
    background: rgb(224, 224, 224);
    border-radius: 10px;
    border: solid 3px #ececece3;

    &::-webkit-slider-runnable-track {
      -webkit-appearance: none;
      transition: box-shadow 0.2s ease-in-out;
    }
    &::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 28px;
      height: 28px;
      box-shadow: inset 0 0 0 40px #555;
      border-radius: 50%;
      transition: box-shadow 0.2s ease-in-out;
    }
  }

  &-text {
    margin-top: 50px;
    font-size: 1.5rem;
    color: #555;
  }
}

.figure_list {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 100px;

  &-item {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 60px;
    height: 60px;
    cursor: pointer;
  }
}

.triangle {
  width: 0;
  height: 0;
  border-width: 30px;
  border-style: solid;

  &--top {
    border-top-color: #555;
    border-bottom: 0;
    border-left-color: transparent;
    border-right-color: transparent;
  }

  &--bottom {
    border-top: 0;
    border-bottom-color: #555;
    border-left-color: transparent;
    border-right-color: transparent;
  }

  &--left {
    border-top-color: transparent;
    border-bottom-color: transparent;
    border-left: 0;
    border-right-color: #555;
  }

  &--right {
    border-top-color: transparent;
    border-bottom-color: transparent;
    border-left-color: #555; 
    border-right: 0; 
  }
}

.arrow {
  position: relative;
  width: 60px;
  height: 30px;
  margin-top: 10px;

  &::before {
    content: "";
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    transform: rotate(45deg);
    width: 30px;
    height: 2px;
    background: #555;
  }

  &::after {
    content: "";
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    transform: rotate(-45deg);
    width: 30px;
    height: 2px;
    background: #555;
  }
}
</style>
