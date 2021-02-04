<template>
  <VGroup v-slot="{ validateGroup }">
    <VTarget
      :validator="inputValidator"
      validateOnInit
      v-slot="{ validate, feedback }"
    >
      <input type="text" v-model="inputValue" @blur="validate" />
      <div class="feedback">{{ feedback }}</div>
    </VTarget>
    <!-- name を指定すると VTarget の外側で feedback を表示する VFeedback が使える -->
    <VTarget
      name="NumberInput"
      :validator="numberInputValidator"
      v-slot="{ validate }"
    >
      <input type="number" v-model="numberValue" @input="validate" />
    </VTarget>
    <VFeedback for="NumberInput" class="feedback" v-slot="{ feedback }">
      {{ feedback }}
    </VFeedback>
    <button @click="validateGroup(onSubmit)">
      送信
    </button>
  </VGroup>
</template>

<script>
import { VGroup, VTarget, VFeedback } from "@/components/Validation"

export default {
  name: "App",
  components: {
    VGroup,
    VTarget,
    VFeedback,
  },
  data() {
    return {
      inputValue: "",
      numberValue: "0",
    }
  },
  methods: {
    inputValidator() {
      return this.inputValue === "" ? "入力してください。" : null
    },
    numberInputValidator() {
      return !this.numberValue || this.numberValue === "4"
        ? "4以外を入力してください。"
        : null
    },
    onSubmit() {
      alert("Success!")
    },
  },
}
</script>

<style scoped>
.feedback {
  color: red;
}
</style>
