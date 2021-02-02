<template>
    <form class="validate-form-container" action="">
        <slot name="default"></slot>
        <div class="submit-area" @click.prevent="submitForm">
            <slot name="submit">
                <button type="submit"
                        class="btn btn-primary"
                >提交</button>
            </slot>
        </div>
    </form>
</template>

<script lang="ts">
import { defineComponent, onUnmounted } from 'vue';
import mitt, {Handler} from "mitt"
export const emitter = mitt()

type ValidateFunc = () => boolean

export default defineComponent({
    name: 'ValidateForm',
    props: {
        msg: String,
    },
    emits: ['formSubmit'],

    setup(props, context) {
        let funcArr: ValidateFunc[] = []
        const submitForm = () => {
            const result = funcArr.map(func => func()).every(result => result)
            context.emit('formSubmit', result);
        }
        const callback = (func: ValidateFunc) => {
            funcArr.push(func)
        }
        emitter.on('form-item-created', callback as Handler)
        onUnmounted(() => {
            emitter.off('form-item-created', callback as Handler)
            funcArr = []
        })

        return {
            submitForm
        }
    }
});
</script>

<style scoped>

</style>
