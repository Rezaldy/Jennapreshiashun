<template>
  <q-page class="row">

  </q-page>
</template>

<script lang="ts">
import ExampleComponent from 'components/ClassComponent.vue'
import { Vue, Component } from 'vue-property-decorator'

@Component({
  components: { ExampleComponent }
})
export default class PageIndex extends Vue {
}
</script>
