<template>
  <div>
    <PersonInput
      v-for="(person, index) of people"
      :person="person"
      :key="index"
      @updatePerson="person = $event"
    />
    <!-- This list will include all errors,
         both from this component and errors from every <PersonInput> -->
    <pre>
            <code>{{ v$ }}</code>
          </pre>
    <div v-for="error of v$.$errors" :key="error.$uid">
      {{ error.$message }}
    </div>
  </div>
</template>

<script>
import { useVuelidate } from "@vuelidate/core";
import { required, minLength } from "@vuelidate/validators";
import PersonInput from "./components/PersonInput.vue";

export default {
  components: { PersonInput },
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      people: [{ name: "John" }, { name: "" }],
    };
  },
  validations: {
    people: {
      required,
      minLength: minLength(3),
    },
  },
};
</script>
