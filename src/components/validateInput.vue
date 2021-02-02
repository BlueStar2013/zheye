<template>
    <div class="validate-input-container pb-3">
        <input  class="form-control"
                :class="{'is-invalid': inputRef.error}"
                @blur="validateInput"
                :value="inputRef.val"
                @input="updateInput"
                v-bind="$attrs"
        >
        <span v-if="inputRef.error" class="invalid-feedback">{{inputRef.message}}</span>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, reactive, onMounted } from 'vue';
import { emitter } from '@/components/ValidateForm.vue'

const emailReg = /^[A-Za-z0-9]+([_\\.][A-Za-z0-9]+)*@([A-Za-z0-9\\-]+\.)+[A-Za-z]{2,6}$/
interface RuleProp {
    type: 'email' | 'required';
    message: string;
}

export type RulesProp = RuleProp[]

export default defineComponent({
    name: 'ValidateInput',
    props: {
        rules: {
            type: Array as PropType<RulesProp>,
        },
        modelValue: String
    },
    inheritAttrs: false,
    setup(props, context) {
        const inputRef = reactive({
            val: props.modelValue || '',
            error: false,
            message: ''
        })

        const updateInput = (e: KeyboardEvent) => {
            const targetVal = (e.target as HTMLInputElement).value
            inputRef.val = targetVal
            context.emit('update:modelValue', targetVal)
        }

        const validateInput = () => {
            if (props.rules) {
                const allPassed = props.rules.every(rule => {
                    let passed = true
                    inputRef.message = rule.message
                    switch (rule.type) {
                        case 'required':
                            passed = (inputRef.val !== '' && inputRef.val.trim() !== '')
                            break
                        case 'email':
                            passed = emailReg.test(inputRef.val)
                            break
                        default:
                            break
                    }
                    return passed
                })
                inputRef.error = !allPassed
                return allPassed
            }
            return true
        }

        onMounted(() => {
            emitter.emit('form-item-created', validateInput)
        })

        return {
            inputRef,
            validateInput,
            updateInput
        }
    }
});
</script>

<style scoped>

</style>
