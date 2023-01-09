<template>
  <div>
    <div>
      <slot name="default" :on="{ open }"></slot>
    </div>
    <q-dialog v-model="dialog">
      <div class="cq-card-date" :class="[`cq-card-date-${id}`]">
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
            <div v-if="error" class="q-mx-sm text-red">
              End date in period can't be before start date !
            </div>
          </div>
          <div>
            <div class="row">
              <div class="col-12 col-md-6">
                <div class="q-pa-md-sm row justify-center">
                  <q-date
                    class="cq-card-date--from"
                    v-model="range.from"
                    minimal
                    flat
                    color="black"
                    :events="eventsFn"
                  >
                  </q-date>
                </div>
              </div>
              <div class="col-12 col-md-6">
                <div class="q-pa-md-sm row justify-center">
                  <q-date
                    flat
                    class="cq-card-date--to"
                    v-model="range.to"
                    minimal
                    color="black"
                    :events="eventsFn"
                    :options="toLimit"
                  >
                  </q-date>
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
                :disable="error"
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
        this.range = { ...this.value };
      }
    }
  },

  data() {
    return {
      id: "",
      dialog: false,
      range: { from: "", to: "" },
      from: "2023/01/01",
      to: "2023/01/04"
    };
  },
  computed: {
    error() {
      return this.range.from > this.range.to ? true : false;
    }
  },
  watch: {
    error(value) {
      if (value) {
        this.range.to = null;
      }
    }
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
      this.range = {};
      this.dialog = false;
    },
    eventsFn(date) {
      setTimeout(() => {
        this.colored("cq-card-date--to");
      }, 0);
      setTimeout(() => {
        this.colored("cq-card-date--from");
      }, 1);

      return date >= this.range.from && date <= this.range.to;
    },
    toLimit(date) {
      return date >= this.range.from && this.range.from ? true : false;
    },
    colored(dateComponentClass) {
      document
        .querySelectorAll(
          `.cq-card-date-${this.id} .${dateComponentClass} .cq-date__range`
        )
        .forEach((el) => {
          el.classList.remove("cq-date__range");
        });
      let end = document.querySelector(
        `.${dateComponentClass} .${dateComponentClass}-end`
      );
      if (end) end.classList.remove(`${dateComponentClass}-end`);
      let start = document.querySelector(
        `.${dateComponentClass} .${dateComponentClass}-start`
      );

      if (start) start.classList.remove(`${dateComponentClass}-start`);

      let days = document.querySelectorAll(
        `.cq-card-date-${this.id} .${dateComponentClass} .q-date__event`
      );
      days.forEach((el) => {
        el.parentElement.parentElement.parentElement.parentElement.classList.add(
          "cq-date__range"
        );
      });
      //
      days[0].parentElement.parentElement.parentElement.parentElement.classList.remove(
        "cq-date__range"
      );
      days[0].parentElement.parentElement.parentElement.parentElement.classList.add(
        `${dateComponentClass}-start`
      );

      days[
        days.length - 1
      ].parentElement.parentElement.parentElement.parentElement.classList.remove(
        "cq-date__range"
      );
      days[
        days.length - 1
      ].parentElement.parentElement.parentElement.parentElement.classList.add(
        `${dateComponentClass}-end`
      );

      //
    }
  },
  mounted() {
    this.id = this._uid;
  }
};
</script>

<style lang="scss">
.q-dialog__inner--minimized > div.cq-card-date {
  width: fit-content;
  max-width: 90vw;
}
.cq-card-date {
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
  .q-date__event {
    background-color: transparent !important;
  }
  .cq-date__range {
    background-color: #f5f5f5;
  }
  .cq-card-date--to-start {
    &::before {
      width: 45%;
      content: "";
      background-color: #f5f5f5;
      top: 0px;
      bottom: 0px;
      position: absolute;
      width: 50%;
      right: 0;
      left: auto;
    }

    .q-btn {
      background-color: #f5f5f5;
    }
  }
  .cq-card-date--from-end {
    &::before {
      width: 45%;
      content: "";
      background-color: #f5f5f5;
      top: 0px;
      bottom: 0px;
      position: absolute;
      width: 50%;
      left: 0;
      right: auto;
    }

    .q-btn {
      background-color: #f5f5f5;
    }
  }
  .cq-card-date--from-start {
    &::before {
      content: "";
      background-color: #f5f5f5;
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      left: 50%;
    }
  }
  .cq-card-date--to-end {
    &::before {
      content: "";
      background-color: #f5f5f5;
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 50%;
    }
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
