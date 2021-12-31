<template>
  <div class="container">
    <div class="title">
      Dạng câu hỏi số 3: Điền câu trả lời ngắn ngọn. Quản lý cần cung cấp câu
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
      <div>
        <div class="dx-fieldset container-field">
          <div class="dx-field">
            <div class="dx-field-label">Đáp án</div>
            <div class="dx-field-value">
              <DxTextArea
                :width="300"
                :height="50"
                v-model:value="dataSrc.answer"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DxTextArea from "devextreme-vue/text-area";
export default {
  components: {
    DxTextArea,
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
        this.$emit("get", newVal, 3);
      },
    },
  },
  data() {
    return {
      dataSrc: {
        question: null,
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

.container {
  border: 1px solid #111;
  padding: 5px;
}
</style>
