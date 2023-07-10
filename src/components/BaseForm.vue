<script lang="ts">
export interface IBase {
  buttons(): VNode[];
}

export class BaseForm implements IBase{
  private onClick() {
    console.log("BASE CLICK");
  }

  public buttons() {
    return [h('button', { onClick: this.onClick }, 'BASE BUTTON')];
  }
}
</script>

<script setup lang="ts">
import { VNode, computed, h, watchEffect } from 'vue';
import CurrentForm from './CurrentForm.vue';

const props = defineProps<{
  formName: string;
}>();

const mapper = {
  'CurrentForm': CurrentForm,
} as { [key: string]: any };

const formRender = computed(() => mapper[props.formName]);

let base: IBase;

if (formRender.value.executor) {
  base = formRender.value.executor;
} else {
  base = new BaseForm();
}

const formButtons = computed(() => base.buttons());

watchEffect(() => console.log(formButtons));


</script>

<template>
  <div>
    <formRender />
  </div>
  <div>
    <template v-for="btn in formButtons">
      <component :is="btn" />
    </template>
  </div>
</template>
