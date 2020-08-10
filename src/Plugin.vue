<template>
  <div>
    <div class="fs-spacing-editor">
      <div class="fs-spacing-editor__bounds">
        <div class="fs-spacing-editor__label">Margin</div>
        <div class="fs-spacing-editor__center">
          <select v-model="model.mt">
            <option
              v-for="key in Object.keys(options)"
              :key="options[key]"
              :value="options[key]"
            >{{ key }}</option>
          </select>
        </div>
        <div class="fs-spacing-editor__flex">
          <div>
            <select v-model="model.ml">
              <option
                v-for="key in Object.keys(options)"
                :key="options[key]"
                :value="options[key]"
              >{{ key }}</option>
            </select>
          </div>
          <div class="fs-spacing-editor__bounds" style="background: #fff;">
            <div class="fs-spacing-editor__label">Padding</div>
            <div class="fs-spacing-editor__center">
              <select v-model="model.pt">
                <option
                  v-for="key in Object.keys(options)"
                  :key="options[key]"
                  :value="options[key]"
                >{{ key }}</option>
              </select>
            </div>
            <div class="fs-spacing-editor__flex">
              <div>
                <select v-model="model.pl">
                  <option
                    v-for="key in Object.keys(options)"
                    :key="options[key]"
                    :value="options[key]"
                  >{{ key }}</option>
                </select>
              </div>
              <div class="fs-spacing-editor__center" style="padding: 1em;">Content</div>
              <div>
                <select v-model="model.pr">
                  <option
                    v-for="key in Object.keys(options)"
                    :key="options[key]"
                    :value="options[key]"
                  >{{ key }}</option>
                </select>
              </div>
            </div>
            <div class="fs-spacing-editor__center">
              <select v-model="model.pb">
                <option
                  v-for="key in Object.keys(options)"
                  :key="options[key]"
                  :value="options[key]"
                >{{ key }}</option>
              </select>
            </div>
          </div>
          <div>
            <select v-model="model.mr">
              <option
                v-for="key in Object.keys(options)"
                :key="options[key]"
                :value="options[key]"
              >{{ key }}</option>
            </select>
          </div>
        </div>
        <div class="fs-spacing-editor__center">
          <select v-model="model.mb">
            <option
              v-for="key in Object.keys(options)"
              :key="options[key]"
              :value="options[key]"
            >{{ key }}</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  methods: {
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: "spacing-editor",
        title: "Spacing Editor",
        description:
          "Allows the user to set top, right, bottom, and left values for padding and margin.",
        options: {
          None: null,
          Tiny: "1",
          Small: "2",
          Regular: "4",
          Large: "8",
          "Extra Large": "16",
        },
      };
    },
    pluginCreated() {
      // eslint-disable-next-line
      console.log(
        "View source and customize: https://github.com/storyblok/storyblok-fieldtype"
      );
    },
  },
  watch: {
    model: {
      handler: function (value) {
        this.$emit("changed-model", value);
      },
      deep: true,
    },
  },
};
</script>
<style>
.fs-spacing-editor {
  /* border: 1px solid #f90; */
  background: #f0f0f0;
  width: 100%;
  overflow: hidden;
}

.fs-spacing-editor select {
  width: 50px;
  overflow: hidden;
}

.fs-spacing-editor__flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.fs-spacing-editor__center {
  text-align: center;
  flex-grow: 1;
}

.fs-spacing-editor__bounds {
  position: relative;
  border: 1px dashed #000;
}

.fs-spacing-editor__label,
.fs-spacing-editor__label {
  position: absolute;
  top: 0;
  left: 0;
  background: #000;
  padding: 2px 4px;
  color: #fff;
  font-size: 0.875rem;
}
</style>