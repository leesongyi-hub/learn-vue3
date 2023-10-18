<template>
  <div>
    <h2>{{ teacher.name }}</h2>
    <h3>강의가 있습니까?</h3>
    <!-- <p>{{ teacher.lectures.length > 2 ? '있음' : '없음' }}</p> -->

    <hr />

    <h3>computed + {{ haslecture }}</h3>
    <h3>computed + {{ haslecture }}</h3>
    <h3>computed + {{ haslecture }}</h3>
    <h3>method + {{ fnhaslecture() }}</h3>
    <h3>method + {{ fnhaslecture() }}</h3>
    <h3>method + {{ fnhaslecture() }}</h3>

    <hr />
    <h3>이름 : {{ fullName }}</h3>
  </div>
</template>

<script>
import { reactive, computed, ref } from "vue";

export default {
  setup () {
    const teacher = reactive ({
      name : '짐코딩',
      lectures: ['HTML/CSS','Javascript','Vue3',]
    })

    //computed -> 캐싱 되기 때문에 성능면에서 더 좋음
    const haslecture = computed(() => {
      console.log('computed');
      return teacher.lectures.length > 2 ? '있음' : '없음'
    });

    //한 줄일때 문법 간략화
    // const haslecture = computed(() =>
    //   teacher.lectures.length > 2 ? '있음' : '없음'
    // )

    //method - > 여러번 호출되기때문에 성능면에서 안 좋음
    const fnhaslecture = () => {
      console.log('method');
      return teacher.lectures.length > 2 ? '있음' : '없음'
    }

    const fistName = ref('홍');
    const lastName = ref('길동');

    //computed는 기본적으로 읽기 전용
    // const fullName = computed(() => fistName.value + ' ' + lastName.value);

    //computed값을 수정하려면 아래처럼 get(), set()을 사용
    const fullName = computed({
      get() {
        return fistName.value + ' ' + lastName.value
      },

      //쓰기 가능
      set(value) {
        [fistName.value, lastName.value] = value.split(' ');
      },
    })

    fullName.value = '이 철수';

    return {
      teacher,
      haslecture,
      fnhaslecture,
      fullName
    };
  }
}
</script>

<style lang="scss" scoped>

</style>