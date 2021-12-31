<template>
  <div>
    <div class="container-header">Form tạo danh sách câu hỏi</div>
    <div class="container-des">
      <div class="dx-fieldset container-field">
        <div class="dx-field">
          <div class="dx-field-label">Tiêu đề:</div>
          <div class="dx-field-value">
            <DxTextArea
              :width="500"
              :height="50"
              v-model:value="dataForm.title"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container-ques">
      <Question1 :data="question1" @get="getDataQuestion" />
      <Question2 :data="question2" @get="getDataQuestion" />
      <Question3 :data="question3" @get="getDataQuestion" />
      <Question4 :data="question4" @get="getDataQuestion" />
    </div>
    <div class="container-btn">
      <DxButton
        :width="100"
        class="btn-export"
        text="Xuất dữ liệu"
        type="normal"
        styling-mode="outlined"
        @click="exportData"
      />
    </div>
  </div>
</template>

<script>
import Question1 from "./components/Question1.vue";
import Question2 from "./components/Question2.vue";
import Question3 from "./components/Question3.vue";
import Question4 from "./components/Question4.vue";
import DxButton from "devextreme-vue/button";
import DxTextArea from "devextreme-vue/text-area";
import _ from "lodash";

export default {
  name: "App",
  components: {
    Question1,
    Question2,
    Question3,
    Question4,
    DxButton,
    DxTextArea,
  },
  data() {
    return {
      question1: {},
      question2: {},
      question3: {},
      question4: {},
      dataForm: {
        title: "",
        steps: [],
      },
    };
  },
  methods: {
    getDataQuestion(dataSrc, type) {
      switch (type) {
        case 1:
          this.question1 = dataSrc;
          break;
        case 2:
          this.question2 = dataSrc;
          break;
        case 3:
          this.question3 = dataSrc;
          break;
        case 4:
          this.question4 = dataSrc;
          break;
        default:
          break;
      }
    },

    exportData() {
      let data = null;
      let me = this;

      if (this.dataForm) {
        data = _.cloneDeep(this.dataForm);
      }

      me.question4.options = me.shuffleCustom(_.cloneDeep(me.question4.answer));

      data["steps"].push({ type: 1, ..._.clone(me.question1) });
      data["steps"].push({ type: 2, ..._.clone(me.question2) });
      data["steps"].push({ type: 3, ..._.clone(me.question3) });
      data["steps"].push({ type: 4, ..._.clone(me.question4) });

      data = {
        trealet: {
          exec: "strealime",
          ...data,
        },
      };

      data = JSON.stringify(data);

      const blob = new Blob([data], { type: "application/json" });

      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "game.trealet";
      link.click();
      URL.revokeObjectURL(link.href);
    },

    shuffleCustom(data) {
      if (!data || data.length == 0) {
        return [];
      }

      let lstKey = [],
        lstVal = [],
        result = [];

      for (let i = 0; i < data.length; i++) {
        lstKey.push(data[i]["key"]);
        lstVal.push(data[i]["value"]);
      }

      lstKey = this.shuffle(lstKey);
      lstVal = this.shuffle(lstVal);

      for (let i = 0; i < data.length; i++) {
        result.push({ key: lstKey[i], value: lstVal[i] });
      }

      return result;
    },

    shuffle(array) {
      let currentIndex = array.length,
        randomIndex;
      while (currentIndex != 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;
        [array[currentIndex], array[randomIndex]] = [
          array[randomIndex],
          array[currentIndex],
        ];
      }

      return array;
    },
  },
};
</script>

<style lang="scss">
body {
  padding: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 10px;
  background-color: gainsboro;
  border-radius: 4px;
}

.container-header {
  text-align: center;
  padding: 15px;
  color: #111;
  font-size: 24px;
}
.container-des {
  border: 1px solid #111;
  padding: 5px;
  background-color: #fff;
}

.container-ques {
  background-color: #fff;
}

.container-btn {
  margin: 20px 10px;
  float: right;
}
</style>
