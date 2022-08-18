<template>
  <input
    v-bind="$attrs"
    :placeholder="label"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :id="uuid"
  >
</template>

<script>
import UniqueID from '../components/UniqueId'
export default {
    props: {
        label: {
            type: String,
            default: ''
        },
        modelValue: {
            type: [String, Number],
            default: ''
        }
    },
    setup() {
        const uuid = UniqueID().getID()
        return {
            uuid
        }
    }
}
</script>