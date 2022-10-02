<script setup>
import { ref } from 'vue';

const colors = ref(['slateblue', 'red', 'purple']);

const vPurple = (el) => {
	el.style.color = 'purple';
};

const vMultiColor = (el, binding) => {
	const colors = binding.value;
	let i = 0;
	setInterval(() => {
		el.style.color = colors[i];
		i++;
		if (i === colors.length) i = 0;
	}, 1000);
};


const vMultiColorWithArgs = (el, binding) => {
  const availablesArgs = {
    normal: 1000,
    slow: 3000,
    crazy: 750
  }
  
  const argSended = binding.arg || 'normal'
  const speedMulticolor = availablesArgs[argSended]  

	let i = 0;
	const colors = binding.value;

	setInterval(() => {
		el.style.color = colors[i];
		i++;
		if (i === colors.length) i = 0;
	}, speedMulticolor);

  if(binding.modifiers.underline){
    el.style.textDecoration = "underline"
  }
};

setTimeout(() => {
  colors.value.push('hotpink')
}, 2500);
</script>

<template>
	<h2 v-purple>Francisco Marín</h2>

	<h2 v-multi-color="colors">
    Francisco Marín
  </h2>

	<h2 v-multi-color-with-args:slow="colors">
    Francisco Marín
  </h2>
  
	<h2 v-multi-color-with-args:crazy.underline="colors">
    Francisco Marín
  </h2>
</template>
