<template>
  <div>
    <div class="fs-spacing-editor">
      <div class="fs-spacing-editor__bounds">
        <div class="fs-spacing-editor__label">Margin</div>
        <div class="fs-spacing-editor__center">
          <select name="mt" v-model="model.mt">
            <option></option>
            <option
              v-for="opt in options"
              :key="model._uid + '_mt_' + opt.id"
              :value="opt.value"
            >
              {{ opt.name }}
            </option>
          </select>
        </div>
        <div class="fs-spacing-editor__flex">
          <div>
            <select name="ml" v-model="model.ml">
              <option></option>
              <option
                v-for="opt in options"
                :key="model._uid + '_ml_' + opt.id"
                :value="opt.value"
              >
                {{ opt.name }}
              </option>
            </select>
          </div>
          <div class="fs-spacing-editor__bounds" style="background: #fff">
            <div class="fs-spacing-editor__label">Padding</div>
            <div class="fs-spacing-editor__center">
              <select name="pt" v-model="model.pt">
                <option></option>
                <option
                  v-for="opt in options"
                  :key="model._uid + '_pt_' + opt.id"
                  :value="opt.value"
                >
                  {{ opt.name }}
                </option>
              </select>
            </div>
            <div class="fs-spacing-editor__flex">
              <div>
                <select name="pl" v-model="model.pl">
                  <option></option>
                  <option
                    v-for="opt in options"
                    :key="model._uid + '_pl_' + opt.id"
                    :value="opt.value"
                  >
                    {{ opt.name }}
                  </option>
                </select>
              </div>
              <div class="fs-spacing-editor__center" style="padding: 1em">
                Content
              </div>
              <div>
                <select name="pr" v-model="model.pr">
                  <option></option>
                  <option
                    v-for="opt in options"
                    :key="model._uid + '_pr_' + opt.id"
                    :value="opt.value"
                  >
                    {{ opt.name }}
                  </option>
                </select>
              </div>
            </div>
            <div class="fs-spacing-editor__center">
              <select name="pb" v-model="model.pb">
                <option></option>
                <option
                  v-for="opt in options"
                  :key="model._uid + '_pb_' + opt.id"
                  :value="opt.value"
                >
                  {{ opt.name }}
                </option>
              </select>
            </div>
          </div>
          <div>
            <select name="mr" v-model="model.mr">
              <option></option>
              <option
                v-for="opt in options"
                :key="model._uid + '_mr_' + opt.id"
                :value="opt.value"
              >
                {{ opt.name }}
              </option>
            </select>
          </div>
        </div>
        <div class="fs-spacing-editor__center">
          <select name="mb" v-model="model.mb">
            <option></option>
            <option
              v-for="opt in options"
              :key="model._uid + '_mb_' + opt.id"
              :value="opt.value"
            >
              {{ opt.name }}
            </option>
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
      };
    },
    async pluginCreated() {
      if (
        this.schema.source === "internal" &&
        this.schema.datasource_slug &&
        this.schema.datasource_slug.length
      ) {
        this.options = await fetchOptionsFromDataSource(this);
      }
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

async function fetchOptionsFromDataSource(context) {
  const endpoint = `cdn/datasource_entries?token=${context.token}&datasource=${context.schema.datasource_slug}&per_page=1000`;
  const response = await context.api.get(endpoint);
  return response.data.datasource_entries;
}
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