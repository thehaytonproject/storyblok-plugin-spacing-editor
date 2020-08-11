<template>
  <div>
    <div class="fs-spacing-editor">
      <div class="fs-spacing-editor__bounds">
        <div class="fs-spacing-editor__label">Margin</div>
        <div class="fs-spacing-editor__center">
          <select name="mt" v-model="model.mt">
            <option
              v-for="opt in selectOptions"
              :key="model._uid + '_mt_' + opt.id"
              :value="opt.value"
            >{{ opt.name }}</option>
          </select>
        </div>
        <div class="fs-spacing-editor__flex">
          <div>
            <select name="ml" v-model="model.ml">
              <option
                v-for="opt in selectOptions"
                :key="model._uid + '_ml_' + opt.id"
                :value="opt.value"
              >{{ opt.name }}</option>
            </select>
          </div>
          <div class="fs-spacing-editor__bounds" style="background: #fff;">
            <div class="fs-spacing-editor__label">Padding</div>
            <div class="fs-spacing-editor__center">
              <select name="pt" v-model="model.pt">
                <option
                  v-for="opt in selectOptions"
                  :key="model._uid + '_pt_' + opt.id"
                  :value="opt.value"
                >{{ opt.name }}</option>
              </select>
            </div>
            <div class="fs-spacing-editor__flex">
              <div>
                <select name="pl" v-model="model.pl">
                  <option
                    v-for="opt in selectOptions"
                    :key="model._uid + '_pl_' + opt.id"
                    :value="opt.value"
                  >{{ opt.name }}</option>
                </select>
              </div>
              <div class="fs-spacing-editor__center" style="padding: 1em;">Content</div>
              <div>
                <select name="pr" v-model="model.pr">
                  <option
                    v-for="opt in selectOptions"
                    :key="model._uid + '_pr_' + opt.id"
                    :value="opt.value"
                  >{{ opt.name }}</option>
                </select>
              </div>
            </div>
            <div class="fs-spacing-editor__center">
              <select name="pb" v-model="model.pb">
                <option
                  v-for="opt in selectOptions"
                  :key="model._uid + '_pb_' + opt.id"
                  :value="opt.value"
                >{{ opt.name }}</option>
              </select>
            </div>
          </div>
          <div>
            <select name="mr" v-model="model.mr">
              <option
                v-for="opt in selectOptions"
                :key="model._uid + '_mr_' + opt.id"
                :value="opt.value"
              >{{ opt.name }}</option>
            </select>
          </div>
        </div>
        <div class="fs-spacing-editor__center">
          <select name="mb" v-model="model.mb">
            <option
              v-for="opt in selectOptions"
              :key="model._uid + '_mb_' + opt.id"
              :value="opt.value"
            >{{ opt.name }}</option>
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
        mt: null,
        mr: null,
        mb: null,
        ml: null,
        pt: null,
        pr: null,
        pb: null,
        pl: null,
      };
    },
    async pluginCreated() {
      if (!this.schema.datasource_slug || !this.schema.datasource_slug.length)
        return;

      const endpoint = `cdn/datasource_entries?token=${this.token}&datasource=${this.schema.datasource_slug}`;

      try {
        const response = await this.api.get(endpoint);
        this.options = response.data.datasource_entries;
      } catch (err) {
        console.log(
          "Could not parse datasource_entries for spacing-editor plugin",
          err
        );
      }
    },
  },
  computed: {
    selectOptions() {
      return this.options.length
        ? this.options
        : [{ id: null, value: null, name: null }];
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
  padding: 2px 4px;
  font-size: 0.875rem;
}
</style>