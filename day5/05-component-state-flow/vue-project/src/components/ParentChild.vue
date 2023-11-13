<template>
  <div>
    <p>{{ myMsg }}</p>
    <p>{{ dynamicProps }}</p>
    <ParentGrandChild 
    :my-msg="myMsg"
    @update-name="updateName"
    />
    <button @click="$emit('someEvent')">클릭</button>
    <button @click="buttonClick">클릭</button>
    <button @click="emitArgs">추가 인자 전달</button>
  </div>
</template>

<script setup>
import ParentGrandChild from '@/components/ParentGrandChild.vue'
// 1. 배열 선언 방식
// defineProps(['myMsg'])

// 2. 객체 선언 방식
// defineProps({
//   myMsg: String,
// })

// props 데이터를 script에서 사용하려면
const props = defineProps({
                myMsg: {
                  type: String,
                  required: true,
                  // validator(value) {
                  //   return ['success', 'warning', 'danger'].includes(value)
                  // }
                  validator(value) {
                    const validValues = ['success', 'warning', 'danger']
                    if (!validValues.includes(value)) {
                      console.error('raise error')
                      return false
                    } 
                    return true
                  }
                },
                dynamicProps: String,
              })

console.log(props)
console.log(props.myMsg)

// emit 선언 방식
const emit = defineEmits(['someEvent', 'emitArgs', 'updateName'])

const updateName = function () {
  emit('updateName')
}

const emitArgs = function () {
  emit('emitArgs', 1, 2, 3)
}

const buttonClick = function () {
  emit('someEvent')
}
</script>

<style scoped>

</style>