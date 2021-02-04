<script>
export default {
  provide() {
    return {
      $validate: this.validate,
      $validateGroup: this.validateGroup,
      $register: this.register,
      $targets: this.targets,
    }
  },
  props: {
    tag: {
      type: String,
      default: "div",
    },
  },
  methods: {
    validate(name) {
      return (this.targets[name].feedback = this.targets[name].validator())
    },
    validateGroup(callback, e) {
      const names = Object.keys(this.targets)
      names.forEach(this.validate)
      const ok = names.every((name) => this.targets[name].feedback === null)
      if (ok) {
        callback(e)
      }
    },
    register(name, validator) {
      this.$set(this.targets, name, {
        feedback: null,
        validator,
      })
    },
  },
  data() {
    return {
      targets: {
        // [name]: { feedback, validator }
      },
    }
  },
  render(h) {
    return h(
      this.tag,
      {},
      this.$scopedSlots.default({
        validateGroup: this.validateGroup,
      }),
    )
  },
}
</script>
