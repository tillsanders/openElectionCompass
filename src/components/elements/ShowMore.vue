<template>
  <div class="show-more" :aria-label="text">
    <span>{{ short }}</span><span v-if="isTruncated">{{ more ? rest : ' ...' }}</span><!-- eslint-disable-line max-len -->
    <a @click="toggle" v-if="isTruncated" class="show-more__toggle">
      &nbsp;{{ $t(more ? 'hide' : 'show').replace(' ', '\xa0') }}
    </a>
  </div>
</template>

<script>
export default {
  name: 'ShowMore',
  data() {
    return {
      more: false,
    };
  },
  props: {
    text: {
      type: String,
      required: true,
    },
    length: {
      type: Number,
      default: 250,
    },
  },
  computed: {
    isTruncated() {
      return this.text.length > this.length;
    },
    short() {
      if (!this.isTruncated) {
        return this.text;
      }
      const truncated = this.text.substr(0, this.length);
      return truncated.substr(0, truncated.lastIndexOf(' '));
    },
    rest() {
      return this.text.substring(this.short.length);
    },
  },
  methods: {
    toggle() {
      this.more = !this.more;
    },
  },
};
</script>

<i18n>
{
  "en": {
    "show": "show more",
    "hide": "hide"
  },
  "de": {
    "show": "weiterlesen",
    "hide": "verbergen"
  }
}
</i18n>

<style lang="scss">
.show-more__toggle {
  font-weight: bold;
  cursor: pointer;
}
</style>
