<template>
  <SpeedInsights />
  <div class="container">
    <div class="bmi-calculator">
      <h1>BMI 计算器 - 在线计算您的体重指数</h1>
      <div class="input-group">
        <label for="height">身高 (cm):</label>
        <input type="number" id="height" v-model.number="height"/>
      </div>
      <div class="input-group">
        <label for="weight">体重 (kg):</label>
        <input type="number" id="weight" v-model.number="weight"/>
      </div>
      <div class="input-group">
        <label class="sexLabel">性别:</label>
        <div>
          <label for="male" class="sex">男</label>
          <input type="radio" id="male" value="男" v-model="gender">
        </div>
        <div>
          <label for="female" class="sex">女</label>
          <input type="radio" id="female" value="女" v-model="gender">
        </div>
      </div>
      <button @click="calculateBMI">计算 BMI</button>
      <p v-if="bmi !== null" class="bmi-explanation">您的 BMI 值为: {{ bmi.toFixed(2) }}</p>
      <div v-if="bmi !== null" >
        <p class="bmi-explanation">{{ bmiExplanation }}</p>
      </div>
    </div>
    <div class="divider"></div>
    <div class="bmi-content">
      <h2>BMI 概念</h2>
      <p>
        身体质量指数（英语：Body Mass Index，简称BMI），是由一个人的质量（体重）和身高计算出的一个数值。
        它有助于帮助您评估自己的健康风险。BMI 被分为四个健康类别之一：过轻、正常、超重和肥胖。
      </p>
      <h2>BMI 计算</h2>
      <p>
        BMI的定义是体重除以身高的平方，以千克/平方米为单位表示，由质量（千克）和身高（米）得出。
        BMI = w / (h * h)，其中 w 为体重；h 为身高。
      </p>
      <h2>BMI 类别</h2>
      <p class="bmi-type">
        1. 体重过轻：BMI 值： 小于 18.5 <br/>
        解读： 体重过轻，可能存在营养不良或身体疾病。建议您咨询医生，进行身体检查，并适当增加营养摄入，改善身体状况。
      </p>
      <p class="bmi-type">
        2. 正常体重：BMI 值： 18.5 - 24 <br/>
        解读： 您的体重处于正常范围，保持良好的生活习惯，包括均衡的饮食和适量的运动，有助于维持健康体重。
      </p>
      <p class="bmi-type">
        3. 体重偏重： BMI 值： 24 - 27 <br/>
        解读： 您的体重偏重，建议您控制饮食，减少高热量、高脂肪的食物摄入，并增加运动量，以降低体重，避免肥胖带来的健康风险。
      </p>
      <p class="bmi-type">
        4. 轻度肥胖：BMI 值： 27 - 30 <br/>
        解读： 您已属于轻度肥胖，建议您尽快采取措施控制体重，包括调整饮食结构、增加运动量，并咨询医生，寻求专业指导。
      </p>
      <p class="bmi-type">
        5. 中度肥胖：BMI 值： 30 - 35 <br/>
        解读： 您已属于中度肥胖，建议您咨询医生，进行身体检查，并制定合理的减重计划，以降低肥胖带来的健康风险。

      </p>
      <p class="bmi-type">
        6. 重度肥胖： BMI 值： 大于 35 <br/>
        解读： 您已属于重度肥胖，建议您尽快就医进行治疗，控制体重，降低肥胖带来的多种疾病风险，例如糖尿病、心血管疾病、关节炎等。
      </p>
      <h2>注意事項</h2>
      <p class="bmi-type">
        BMI 指标只是一个参考值，无法完全反映个体健康状况。<br/>
        不同的人群，例如运动员、孕妇等，其 BMI 值的解读标准可能有所不同。<br/>
        如果您对自己的体重状况存在疑问，建议您咨询医生进行专业评估。
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { SpeedInsights } from '@vercel/speed-insights/vue';

export default {
  data() {
    return {
      weight: 70,
      height: 175,
      gender: "男",
      bmi: null,
      bmiExplanation: null,
    };
  },
  methods: {
    calculateBMI() {
      if (this.height === 0) {
        this.bmi = 0;
      } else {
        this.bmi = this.weight / (this.height * this.height / 10000);
      }
      if (this.bmi === 0) {
        this.bmiExplanation = "身高或体重异常，请重新输入。";
      } else if (this.bmi > 0 && this.bmi < 18.5) {
        this.bmiExplanation = "过轻，建议您适当增加营养摄入。";
      } else if (this.bmi >= 18.5 && this.bmi < 24) {
        this.bmiExplanation = "正常，保持良好的生活习惯。";
      } else if (this.bmi >= 24 && this.bmi < 27) {
        this.bmiExplanation = "偏重，建议您控制饮食并适当运动。";
      } else if (this.bmi >= 27 && this.bmi < 30) {
        this.bmiExplanation = "轻度肥胖，建议您尽快采取措施控制体重。";
      } else if (this.bmi >= 30 && this.bmi < 35) {
        this.bmiExplanation = "中度肥胖，建议您咨询医生寻求专业指导。";
      } else if (this.bmi >= 35) {
        this.bmiExplanation = "重度肥胖，建议您尽快就医进行治疗。";
      }
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between; /* 左右两侧内容等间距 */
}

.divider {
  height: 960px;
  width: 1px;
  background-color: #ccc;
  margin: 80px 0; /* 添加上下边距 */
}

.bmi-calculator {
  margin: 350px 50px auto auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  text-align: center;
  font-family: sans-serif;
}

.bmi-content {
  width: 800px;
  margin: auto auto auto 50px;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
  font-family: sans-serif;
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.input-group {
  margin-bottom: 15px;
  display: flex;
  align-items: center;
}

label {
  margin-right: 10px;
  font-weight: bold;
  text-align: right;
  width: 120px; /* 调整 label 宽度 */
  display: inline-block; /* 允许 label 撑开宽度 */
}

.sexLabel {
  width: 85px;
}

.sex {
  width: 85px;
}


input[type="number"] {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 3px;
  margin-left: 10px;
}

button {
  width: 100%;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

h2 {
  text-align: left;
}

p {
  text-indent: 2em;
  text-align: left;
  font-size: 18px;
  margin-top: 20px;
  color: #555;
}

.bmi-type {
  text-indent: 0;
}

.bmi-explanation {
  margin-rigth: 100px;
  color: hotpink;
  : hotpink;
  text-align: center;
}
</style>
