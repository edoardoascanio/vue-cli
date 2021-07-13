<template>
    <div class="mb-3">
        <label class="form-label">
            {{label}}
        </label>

        <textarea  
            class="form-control"
            :type="inputType"
            :placeholder="placeholder"
            :value="value"
            @input="$emit('input', $event.currentTarget.value)">
        </textarea>

        <input 
      
        />
    </div>
</template>

<script>
export default {
    name: "textInput",
    props: {
        label: String,
        value: String,
        placeholder: String,
        inputType: {
            type: String,
            default: "text",
        },
    }
}
</script>