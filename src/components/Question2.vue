<template>
  <div class="container">
    <div class="title">
      Câu hỏi số 2: Trả lời câu hỏi dạng A, B, C, D. Quản lý cần cung cấp câu
      hỏi liên quan đến đồ vật đã tìm kiếm được trong câu hỏi số 1.
    </div>
    <div>
      <div class="dx-fieldset container-field">
        <div class="dx-field">
          <div class="dx-field-label">Câu hỏi:</div>
          <div class="dx-field-value">
            <DxTextArea
              :width="400"
              :height="100"
              v-model:value="dataSrc.question"
            />
          </div>
        </div>
      </div>
    </div>
    <div>
      <div>Các đáp án:</div>
      <div>
        <div class="dx-fieldset container-field">
          <div class="dx-field">
            <div class="dx-field-label">Đáp án A:</div>
            <div class="dx-field-value">
              <DxTextArea
                :width="300"
                :height="50"
                v-model:value="dataSrc['options'][0]"
              />
            </div>
          </div>
        </div>
        <div class="dx-fieldset container-field">
          <div class="dx-field">
            <div class="dx-field-label">Đáp án B:</div>
            <div class="dx-field-value">
              <DxTextArea
                :width="300"
                :height="50"
                v-model:value="dataSrc['options'][1]"
              />
            </div>
          </div>
        </div>
        <div class="dx-fieldset container-field">
          <div class="dx-field">
            <div class="dx-field-label">Đáp án C:</div>
            <div class="dx-field-value">
              <DxTextArea
                :width="300"
                :height="50"
                v-model:value="dataSrc['options'][2]"
              />
            </div>
          </div>
        </div>
        <div class="dx-fieldset container-field">
          <div class="dx-field">
            <div class="dx-field-label">Đáp án D:</div>
            <div class="dx-field-value">
              <DxTextArea
                :width="300"
                :height="50"
                v-model:value="dataSrc['options'][3]"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="dx-fieldset container-field-1">
      <div class="dx-field">
        <div class="dx-field-label">
          Đáp án của câu hỏi(A - 1, B - 2, C - 3, D - 4):
        </div>
        <div class="dx-field-value">
          <DxTextBox
            :width="100"
            :max-length="50"
            v-model:value="dataSrc.answer"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DxTextArea from "devextreme-vue/text-area";
import DxTextBox from "devextreme-vue/text-box";
export default {
  components: {
    DxTextArea,
    DxTextBox,
  },
  props: {
    data: {
      type: Object,
      default: null,
    },
  },
  emits: ["get"],
  watch: {
    dataSrc: {
      deep: true,
      handler: function (newVal) {
        this.$emit("get", newVal, 2);
      },
    },
  },
  data() {
    return {
      dataSrc: {
        question: null,
        options: ["", "", "", ""],
        answer: null,
      },
    };
  },
};
</script>
<style lang="scss" scoped>
.container-field {
  max-width: 500px;
}
.container-field-1 {
  .dx-field-label {
    width: 60% !important;
  }
  .dx-field-value {
    width: 40% !important;
  }
  max-width: 600px;
}

.container {
  border: 1px solid #111;
  padding: 5px;
}
</style>
