<template>
  <div>
    <div>
      <slot name="default" :on="{ open }"></slot>
    </div>
    <q-dialog v-model="dialog">
      <div class="cq-card-date">
        <div class="cq-card-date--section">
          <div class="row items-center">
            <q-btn
              class="cq-card-date--button"
              padding="xs"
              unelevated
              color="grey-11"
            >
              <q-icon color="black" :size="'sm'" name="mdi-calendar-blank" />
            </q-btn>
            <div class="q-mx-sm text-weight-bold">Report Period</div>
          </div>
          <div>
            <div
              class="c-flex c-flex-column c-justify-space-between c-flex-lg-row"
            >
              <div class="c-w-lg-50">
                <div class="column wrap justify-center full-height q-px-lg">
                  <div class="q-mb-sm">
                    <q-input
                      label="from"
                      color="black"
                      outline
                      v-model="range.from"
                    ></q-input>
                  </div>
                  <div>
                    <q-input
                      label="to"
                      color="black"
                      outline
                      v-model="range.to"
                    ></q-input>
                  </div>
                </div>
              </div>
              <div class="">
                <div>
                  <q-date
                    flat
                    minimal
                    color="black"
                    range
                    v-model="range"
                  ></q-date>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="cq-card-date--actions">
          <div class="row">
            <div class="col">
              <q-btn
                @click="cancel()"
                color="black"
                outline
                class="full-width cq-card-date--button"
                >Cancel</q-btn
              >
            </div>
            <div style="margin-inline: 8px"></div>
            <div class="col">
              <q-btn
                color="black"
                unelevated
                @click="save()"
                class="full-width cq-card-date--button"
                >save</q-btn
              >
            </div>
          </div>
        </div>
      </div>
    </q-dialog>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Object
    }
  },
  watch: {
    dialog(value) {
      console.log(value);
      if (value) {
        this.range = this.value;
      }
    }
  },
  computed: {
    // range: {
    //   get() {
    //       return this.value
    //   },
    //   set(value) {
    //       this.$emit('input',value)
    //     }
    //   }
  },
  data() {
    return {
      dialog: false,
      range: { from: "", to: "" }
    };
  },
  methods: {
    open() {
      this.dialog = true;
    },
    save() {
      this.$emit("input", this.range);
      this.dialog = false;
    },
    cancel() {
      this.dialog = false;
      this.range = { from: "", to: "" };
    }
  }
};
</script>

<style lang="scss">
.cq-card-date {
  width: 900px;
  max-width: 90vw;
  border-radius: 14px !important;

  .cq-card-date--section {
    padding-inline: 10px;
    padding-top: 10px;
    background-color: rgb(255, 255, 255);
    border-start-start-radius: 14px !important;
    border-start-end-radius: 14px !important;
  }
  .cq-card-date--actions {
    padding-block: 10px;
    padding-inline: 10px;
    background-color: rgb(247, 247, 247);
    border-end-start-radius: 14px !important;
    border-end-end-radius: 14px !important;
  }
  .cq-card-date--button {
    border-radius: 8px;
  }
}
</style>
<style>
.c-flex {
  display: flex;
}
.c-justify-space-between {
  justify-content: space-between;
}
.c-flex-column {
  flex-direction: column;
}
@media (min-width: 1200px) {
  .c-flex-column.c-flex-lg-row {
    flex-direction: row;
  }
  .c-w-lg-50 {
    width: 50%;
  }
}
</style>
