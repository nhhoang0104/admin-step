<template>
  <div class="container">
    <div class="title">Dạng câu hỏi số 4:Nối .</div>
    <div class="dx-fieldset container-field">
      <div class="dx-field">
        <div class="dx-field-label">Câu hỏi</div>
        <div class="dx-field-value">
          <DxTextArea
            :width="500"
            :height="50"
            v-model:value="dataSrc.question"
          />
        </div>
      </div>
    </div>
    <div class="item-container">
      <div v-for="item in dataSrc['answer']" :key="item.index" class="item">
        <div>Cột A - Cột B:</div>
        <div class="item-content">
          <DxTextArea
            :width="400"
            :height="80"
            v-model:value="dataSrc['answer'][item.index].key"
          />
          <DxTextArea
            :width="400"
            :height="80"
            v-model:value="dataSrc['answer'][item.index].value"
          />
        </div>
      </div>
      <!-- <DxButton
        :width="100"
        class="btn-add"
        text="Thêm"
        type="normal"
        styling-mode="outlined"
        @click="add"
      /> -->
    </div>
  </div>
</template>
<script>
import DxTextArea from "devextreme-vue/text-area";
//import DxButton from "devextreme-vue/button";
export default {
  components: { DxTextArea },
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
        this.$emit("get", newVal, 4);
      },
    },
  },
  data() {
    return {
      dataSrc: {
        question: "",
        answer: [
          { index: 0, key: null, value: null },
          { index: 1, key: null, value: null },
          { index: 2, key: null, value: null },
          { index: 3, key: null, value: null },
        ],
        options: [],
      },
    };
  },
  methods: {
    add() {
      let length = this.dataSrc.length || 0;
      if (length === 0) {
        this.dataSrc = [];
      }
      this.dataSrc.push({ index: length, key: null, value: null });
    },
  },
};
</script>
<style lang="scss">
.item-container {
  .item {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 10px;

    .item-content {
      display: flex;
      gap: 20px;
    }
  }
}

.title {
  margin: 10px 0px;
}

.container {
  border: 1px solid #111;
  padding: 5px;
}

.container-field {
  max-width: 700px;
}
</style>
