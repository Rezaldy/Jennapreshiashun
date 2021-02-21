<template>
  <q-item
    clickable
    @click="gotoRoute(route)"
  >
    <q-item-section
      v-if="icon"
      avatar
    >
      <q-icon :name="icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
      <q-item-label caption>
        {{ caption }}
      </q-item-label>
    </q-item-section>
  </q-item>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class EssentialLink extends Vue {
  @Prop({ type: String, required: true }) readonly title!: string;
  @Prop({ type: String, default: '' }) readonly caption!: string;
  @Prop({ type: String, default: '' }) readonly route!: string;
  @Prop({ type: String, default: '' }) readonly icon!: string;

  gotoRoute (route: string) {
    if (route.length) {

    } else {
      this.$q.notify({
        type: 'warning',
        position: 'bottom-right',
        message: 'This route is empty!',
        actions: [
          { label: 'Dismiss', color: 'black', handler: () => { /* ... */ } }
        ]
      })
    }
  }
}
</script>
