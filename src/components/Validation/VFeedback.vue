<script>
export default {
  inject: ["$targets"],
  props: {
    for: {
      type: String,
      required: true,
    },
    tag: {
      type: String,
      default: "div",
    },
  },
  computed: {
    feedback() {
      return this.$targets && this.$targets[this.for]
        ? this.$targets[this.for].feedback
        : null
    },
  },
  render(h) {
    return h(
      this.tag,
      {},
      this.$scopedSlots.default({
        feedback: this.feedback,
      }),
    )
  },
}
</script>
