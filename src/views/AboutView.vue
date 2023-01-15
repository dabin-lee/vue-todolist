<template>
  <h1>{{ getDateAndTime(createAt) }}</h1>

  <div class="row g-3">
    <!-- <div class="col-4"> -->
    <card-view>
      <template v-slot:header>
        <h2>1. marke a string out of an array</h2>
      </template>
      <template v-slot:default>
        <p>{{ arr1 }}</p>
        <p style="color: white">join()</p>
      </template>
    </card-view>
    <card-view>
      <template v-slot:header>
        <h2>2. marke an array out of string</h2>
      </template>
      <template v-slot:default>
        <p>{{ arr2 }}</p>
        <p style="color: white">split()</p>
      </template>
    </card-view>

    <card-view>
      <template v-slot:header>
        <h2>3. marke this array [ "apple", "orange", "banana" ]</h2>
      </template>
      <template v-slot:default>
        <p style="color: white">reverse()</p>
        <p>{{ arr3 }}</p>
      </template>
    </card-view>

    <card-view>
      <template v-slot:header>
        <h2>4. make new array without the first two element</h2>
      </template>
      <template v-slot:default>
        <p style="color: white">splice()</p>
        <p>{{ arr4 }}</p>
        <p>
          slice(): 새로운 배열을 만듬 <br />
          - end숫자는 exclusive임을 기억해야한다. 0 2라고 지정하면 마지막 2는
          배제가 되어 0 1까지만 전달된다.
        </p>
      </template>
    </card-view>
    <card-view>
      <template v-slot:header>
        <h2>5. 평균점수 구하기</h2>
      </template>
      <template v-slot:default>
        <p style="color: white">splice()</p>
        <p>1) score가 90점 이상인 학생:{{ arr5 }}</p>
        <p>2) enrolled가 true인 학생:{{ arr6 }}</p>
        <p>3) 학생들의 점수만 뽑은 배열:{{ arr7 }}</p>
        <p>4) 학생들의 점수만 뽑은 배열:{{ arr7 }}</p>
        <p>5) score가 50점 이하인 학생이 있나요?:{{ arr8 }}</p>
        <p>6) 학생들의 평균점수:{{ arr9 }}</p>
        <p>7) 학생들의 점수 string으로 바꾸기:{{ arr10 }}</p>
        <p>8) 낮은 점수별로 정렬:{{ arr11 }}</p>
      </template>
    </card-view>
  </div>
  <!-- </div> -->
</template>
<script>
import { dataFormat } from "../mixins/dateFormat";
import CardView from "../slot/CardView.vue";
export default {
  components: {
    CardView,
  },
  data() {
    return {
      createAt: {},
      fruits: ["banana", "orange", "apple"],
      fruits2: "사과, 키위, 바나나, 체리",
      numberArr: [1, 2, 3, 4, 5],
      students: [
        { name: "a", age: 29, enrolled: true, score: 45 },
        { name: "b", age: 28, enrolled: false, score: 80 },
        { name: "c", age: 30, enrolled: true, score: 90 },
        { name: "d", age: 40, enrolled: false, score: 66 },
        { name: "e", age: 18, enrolled: true, score: 88 },
      ],
    };
  },
  // method: {
  //   getDateAndTime(date) {
  //     let hour = date.getHours();
  //     let minutes = date.getMinutes();
  //     let fullDate = `${date.getFullYear()} / ${
  //       date.getMonth() + 1
  //     } / ${date.getDate()}`;
  //     return `${fullDate} ${hour}: ${minutes}`;
  //   },
  // },
  created() {
    this.createAt = new Date();
  },
  mixins: [dataFormat],
  computed: {
    arr1: function () {
      return this.fruits.join("|");
    },
    arr2: function () {
      // return this.fruits2.split(",");
      //string을 받아서 배열로 만듬 첫번째 인자는 구분자가 들어간다.
      return this.fruits2.split(",", 2);
      //(옵셔널)두번째인자는 limit: 출력하는 개수를 정함
    },
    arr3: function () {
      return this.fruits.reverse();
    },
    arr4: function () {
      const newArr = this.numberArr.slice(2, 5);
      return newArr;
    },
    arr5: function () {
      // return this.students.find((student) => student.score >= 90);
      return this.students.find((student) => student.score === 90);
    },
    arr6: function () {
      const result = this.students.filter((student) => student.enrolled);
      return result.length;
      //filter는 filtering된 새로운 배열을 전달한다.
    },
    arr7: function () {
      const result = this.students.map((student) => student.score);
      return result;
      // map: 배열에 있는 요소 한가지 한가지를 다른것으로 맵핑해준다.
      // 세가지 아이템이 들어있는 배열을 각각의 요소를 함수를 거쳐 새로운 값으로 맵핑되어 만들어진다.
    },
    arr8: function () {
      // const result = this.students.some((student) => student.score < 50);
      // return result;
      // 50점 이하인 학생이 있는지 확인하는 문제
      // 이미 결과값은 있기때문에 true, false로 확인하는 방법이 더 빠르다.
      // some: 배열에 있는 요소 하나하나 검사 중 하나라도 요건에 맞으면 true가 출력된다.

      const result = !this.students.every((student) => student.score >= 50);
      return result;
      //every: 모든 요소가 조건이 충족되어야 true를 리턴한다.
      // (모든 학생들의 점수가 50점이 이하 여야지만 true가 리턴된다. )
    },
    arr9: function () {
      const result = this.students.reduce((prev, curr) => {
        return prev + curr.score;
        // curr: 배열 하나하나씩 전달된다.
        // prev: curr값이 하나씩 하나씩 전달 받아 누적된다. .
      }, 0);
      return result / this.students.length;
      // 콜백함수 리턴 값 전달, 초기값 전달
      // 콜백함수에서 리턴된 값은 누적된 값을 전달한다.
      // 배열에 있는 값을 누적해서 사용한다.
      // reduceRight: 배열의 제일 뒤에서 시작됨
    },

    arr10: function () {
      // return this.students.map((student) => student.score).join();
      // 배열을 점수로 반환하기 위해 map을 위해 새로운 배열을 만든다.
      // 리턴된 새로운 배열을 string으로 변환시킴
      return this.students
        .map((student) => student.score)
        .filter((scroe) => scroe >= 50)
        .join();
    },
    arr11: function () {
      const result = this.students
        .map((student) => student.score)
        .sort()
        .join();
      return result;
    },
  },
};
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
