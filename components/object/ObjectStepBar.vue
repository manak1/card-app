<template>
  <div class="w-full py-6">
    <div class="flex">
      <div v-for="step in steps" :key="step.index" class="w-1/4">
        <div class="relative mb-2">
          <template v-if="step.isBar">
            <div
              class="absolute flex align-center items-center align-middle content-center"
              style="
                width: calc(100% - 2.5rem - 1rem);
                top: 50%;
                transform: translate(-50%, -50%);
              "
            >
              <div
                class="w-full bg-gray-200 rounded items-center align-middle align-center flex-1"
              >
                <div
                  class="w-0 bg-green-300 py-1 rounded"
                  :class="activeBarClass(step)"
                ></div>
              </div>
            </div>
          </template>
          <div
            class="w-10 h-10 mx-auto rounded-full text-lg text-white flex items-center"
            :class="activeCircleClass(step)"
          >
            <i
              class="flex justify-center items-center w-full"
              :class="`c-icon__${step.icon}`"
            ></i>
          </div>
        </div>
        <div class="text-xs text-center md:text-base">
          {{ step.label }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      steps: [
        {
          id: 1,
          icon: "name",
          label: "お名前",
          isBar: false,
          state: "step1",
        },
        {
          id: 2,
          icon: "sns",
          label: "SNS",
          isBar: true,
          state: "step2",
        },
        {
          id: 3,
          icon: "company",
          label: "会社情報",
          isBar: true,
          state: "step3",
        },
        {
          id: 4,
          icon: "download",
          label: "ダウンロード",
          isBar: true,
          state: "step4",
        },
      ],
    }
  },
  computed: {
    target() {
      const targetRoute = this.$route.name
      const targetStep = targetRoute.split("-")[2]
      return this.steps.find((value) => value.state === targetStep)
    },
  },
  methods: {
    activeBarClass(item) {
      const targetData = this.target
      return {
        bar: item.id <= targetData.id,
      }
    },
    activeCircleClass(item) {
      const targetData = this.target
      return {
        "bg-green-500": item.id <= targetData.id,
        "border-2": item.id > targetData.id,
        "border-gray-200": item.id > targetData.id,
        "bg-white": item.id > targetData.id,
      }
    },
  },
}
</script>

<style scoped>
.c-icon__name::before {
  content: "";
  background-size: contain;
  background-repeat: no-repeat;
  display: inline-block;
  width: 24px;
  height: 26px;
  background-image: url("~assets/images/baseline_phone_iphone_black_18dp.png");
}
.c-icon__sns::before {
  content: "";
  background-size: contain;
  background-repeat: no-repeat;
  display: inline-block;
  width: 24px;
  height: 24px;
  background-image: url("~assets/images/baseline_phone_iphone_black_18dp.png");
}

.c-icon__company::before {
  content: "";
  background-size: contain;
  background-repeat: no-repeat;
  display: inline-block;
  width: 24px;
  height: 24px;
  background-image: url("~assets/images/baseline_phone_iphone_black_18dp.png");
}

.c-icon__download::before {
  content: "";
  background-size: contain;
  background-repeat: no-repeat;
  display: inline-block;
  width: 24px;
  height: 24px;
  background-image: url("~assets/images/baseline_phone_iphone_black_18dp.png");
}
.bar {
  width: 100%;
}
</style>
