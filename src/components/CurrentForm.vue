<script lang="ts">

class CurrentForm implements IBase {

  public buttons(): VNode[] {
    console.log(this);
    return [h('button', { onClick: this.action }, 'CURRENT BUTTON')]
  }

  public action() {
    console.log("action");
  }
}

</script>

<script setup lang="ts">
import { VNode, h } from 'vue';
import { IBase } from './BaseForm.vue';

defineOptions({
  executor: new CurrentForm(),
})

</script>

<template>
  <div>
    <h3>Some content here</h3>
  </div>
</template>
