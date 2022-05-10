# Forms in Vue

[Vue - The Complete Guide, Section 11](https://www.udemy.com/course/vuejs-2-the-complete-guide/)

1. `submit.prevent`
   When form submission occurs, prevent the browser default, which would be that a request is sent and result in a page reload.
2. In vanilla JavaScript or if you use $refs to fetch the input data, despite the input type, the input data is always stored as string
   When use `v-model` bind a number input to a state, `v-model` will automactically convert the user input from string to number. With .number modifier, you can force v-model convert other types of input to a number.
   总之，使用$ref 绑定数字输入框无类型转换，得到 string, 使用 v-model 绑定数字输入有类型转换，得到 number
3. When you use v-model bind checkboxes or radio buttons, you need bind to every input in the same group, add different value attribute to each input, and set the initial value of bound state of checkboxes and radios to empty array and null respectively.
4. v-model with a single separate checkbox: set the initial value of bound state to false
5. Build a custom form control component
   When used on <input>, v-model is substitue for the combination of `@input` and `:value`
   When used on custom component, v-model is substitue for combination of `@update:modelValue` and `:model-value`

   ```js
   // in TheForm.vue
   <RatingControl v-model='rating'> // bind rating to modelValue

   export default{
       data(){
           return{
               rating:null
           }
       }
   }
   ```

   ```js
   // in RatingControl.vue
   <ul>
        // when modelValue(and rating in parent component) is chosed, we can add 'active' class to corresponding item
        <li :class="{ active: modelValue === 'poor' }">
            // when user clicks a button, update modelValue to 'poor' through update:modelValue method, therefore `rating` in parent component is updated
            <button type="button" @click="$emit('update:modelValue','poor')">Poor</button>
        </li>
        <li :class="{ active: modelValue === 'average' }">
            <button type="button" @click="$emit('update:modelValue','average')">Average</button>
         </li>
        <li :class="{ active: modelValue === 'great' }">
            <button type="button" @click="$emit('update:modelValue','great')">Great</button>
        </li>
   </ul>

   export default{
      props:['modelValue'],
      emits:['update:modelValue']

   }
   ```
