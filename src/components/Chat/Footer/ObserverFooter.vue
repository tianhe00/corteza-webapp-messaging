<template>
  <div>
    <footer>
      <h3>
        {{ $t('channel.observing', { label: getLabel(channel) }) }}
      </h3>

      <button
        v-if="channel.canJoin"
        class="btn btn-green"
        @click="onJoin"
      >
        {{ $t('channel.join') }}
      </button>
    </footer>
  </div>
</template>
<script>

/**
 * Component defines a footer that should be shown to non-members (observers).
 */
export default {
  props: {
    channel: {
      type: Object,
      required: true,
    },
  },

  methods: {
    /**
     * Handles channel joining.
     */
    onJoin () {
      this.$MessagingAPI.channelJoin({
        channelID: this.channel.channelID,
        userID: this.$auth.user.userID,
      })
    },
  },
}
</script>

<style scoped lang="scss">
@import 'corteza-webapp-messaging/src/themes/corteza-base/btns.scss';

footer {
  text-align: center;
  width: 100%;
  height: 80px;
  border-top: 2px solid $secondary;
  background-color: $white;
}
</style>
