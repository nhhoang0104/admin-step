<template>
  <div class="container">
    <div class="title">
      Dạng câu hỏi số 1: Tìm kiếm đồ vật theo hình ảnh để trả lời câu hỏi phía
      sau. Quản lý cần cung cấp hình ảnh của món đồ vật cần tìm.
    </div>
    <div class="dx-fieldset container-field">
      <div class="dx-field">
        <div class="dx-field-label">Câu hỏi</div>
        <div class="dx-field-value">
          <DxTextArea :width="300" :height="50" v-model:value="dataSrc.title" />
        </div>
      </div>
    </div>
    <div class="dx-fieldset container-field">
      <div class="dx-field">
        <div class="dx-field-label">Id của hình ảnh:</div>
        <div class="dx-field-value">
          <DxTextBox
            :width="100"
            :max-length="50"
            v-model:value="dataSrc['imgId']"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DxTextBox from "devextreme-vue/text-box";
import DxTextArea from "devextreme-vue/text-area";
export default {
  components: {
    DxTextBox,
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
        this.$emit("get", newVal, 1);
      },
    },
  },
  data() {
    return {
      dataSrc: {
        title: null,
        imgId: null,
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
