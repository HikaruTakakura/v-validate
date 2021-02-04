<script>
let count = 0

export default {
  inject: ["$register", "$validate", "$targets"],
  props: {
    name: String,
    validator: Function,
    tag: {
      type: String,
      default: "div",
    },
    // if true validate on created hook
    validateOnInit: {
      type: Boolean,
      default: false,
    },
  },
  created() {
    this._name = this.name ? this.name : "Target_" + count++
    this.$register(this._name, this.validator)
    if (this.validateOnInit) {
      this.$validate(this._name)
    }
  },
  methods: {
    validate() {
      this.$validate(this._name)
    },
  },
  computed: {
    feedback() {
      return this.$targets && this.$targets[this._name]
        ? this.$targets[this._name].feedback
        : null
    },
  },
  render(h) {
    return h(
      this.tag,
      {},
      this.$scopedSlots.default({
        validate: this.validate,
        feedback: this.feedback,
      }),
    )
  },
}
</script>
