<template>
  <div
    class="h-screen min-w-screen flex items-center justify-center relative overflow-hidden"
  >
    <!-- <div class="absolute inset-0 bg-wave-top bg-no-repeat bg-top -z-10"></div> -->
    <div class="absolute inset-0 bg-wave bg-no-repeat bg-bottom -z-10"></div>
    <div class="flex flex-col gap-y-6">
      <!-- <UStep v-model="step" :total-step="totalStep" /> -->
      <div class="relative">
        <transition
          leave-to-class="opacity-0 transition-all translate-y-full -translate-x-full -rotate-6 duration-[1000ms] absolute"
          enter-from-class="opacity-0 transition-all -translate-y-full translate-x-full rotate-6 duration-[1000ms] h-0"
          enter-to-class="opacity-1 transition-all rotate-0 duration-[1000ms]"
          :duration="1000"
        >
          <component
            :is="viewPort[step - 1].component"
            :btnText="viewPort[step - 1].btnText"
            @next="viewPort[step - 1].onSubmit"
            :user-data="userData"
          />
        </transition>
      </div>
    </div>
  </div>
</template>
<script>
import UStep from "~/components/UStep.vue";
import GettingStarted from "~/components/Welcome/GettingStarted.vue";
import AcceptLocation from "~/components/Welcome/AcceptLocation.vue";
import AcceptNotification from "~/components/Welcome/AcceptNotification.vue";
import AcceptNetworkManager from "~/components/Welcome/AcceptNetworkManager.vue";
import StartSetup from "~/components/Welcome/StartSetup.vue";
import StartSignup from "~/components/Welcome/StartSignup.vue";
export default {
  components: {
    GettingStarted,
    UStep,
    AcceptLocation,
    AcceptNotification,
    AcceptNetworkManager,
    StartSetup,
    StartSignup,
  },
  data() {
    return {
      userData: {},
      step: 1,
      totalStep: 4,
      viewPort: [
        {
          component: "GettingStarted",
          btnText: "Tiếp tục",
          onSubmit: this.next,
        },
        {
          component: "AcceptLocation",
          btnText: "Tiếp tục",
          onSubmit: this.next,
        },
        {
          component: "AcceptNotification",
          btnText: "Tiếp tục",
          onSubmit: this.next,
        },
        {
          component: "AcceptNetworkManager",
          btnText: "Tiếp tục",
          onSubmit: this.next,
        },
        {
          component: "StartSignup",
          btnText: "Hoàn tất",
          onSubmit: this.next,
        },
        {
          component: "StartSetup",
          onSubmit: this.setupDone,
        },
      ],
    };
  },
  methods: {
    next(data) {
      this.step += 1;
      this.userData = { ...this.userData, ...data };
    },
  },
};
</script>
