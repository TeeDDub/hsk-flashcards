<template>
    <div class="bg-white rounded-lg shadow-lg p-6">
        <div class="flex flex-wrap">
            <div class="w-full md:w-1/4 font-bold" style="font-size: 5rem;">{{ entry }}</div>
            <div class="w-full md:w-1/2">
                <div class="h-1/3"><p><b>품사</b></p><p id="parts" style="font-size: 1.2rem;" :class="{ hide: hideParts }"> {{ parts.join(', ') }}</p></div>
                <div class="h-1/3"><p><b>발음</b></p><p id="pron" style="font-size: 1.2rem;" :class="{ hide: hidePron }"> {{ pron }}</p></div>
                <div class="h-1/3"><p><b>의미</b></p><p id="means" style="font-size: 1.2rem;" :class="{ hide: hideMeans }"> {{ means.join(', ') }}</p></div>
            </div>
            <div class="w-full md:w-1/4 mt-4">
				<label for="hideParts">
					<div class="w-full inline-block md:h-1/3 cursor-pointer py-1 md:py-0">
						<b>품사 가리기</b>:<input id="hideParts" type="checkbox" v-model="hideParts">
					</div>
				</label>
				<label for="hidePron">
					<div class="w-full inline-block md:h-1/3 cursor-pointer py-1 md:py-0">
						<b>발음 가리기</b>:<input id="hidePron" type="checkbox" v-model="hidePron">
					</div>
				</label>
				<label for="hideMeans">
					<div class="w-full inline-block md:h-1/3 cursor-pointer py-1 md:py-0">
						<b>의미 가리기</b>:<input id="hideMeans" type="checkbox" v-model="hideMeans">
					</div>
				</label>
            </div> 
        </div>
    </div>
</template>

<script>

export default {
    name: 'FlashCard',
    props: {
        entry: {
            type: String,
            required: true
        },
        parts: {
            type: Array,
            required: true
        },
        pron: {
            type: String,
            required: true
        },
        means: {
            type: Array,
            required: true
        }
    },
    data() {
    return {
      hideParts: false,
      hidePron: false,
      hideMeans: false,
    };
  },
}
</script>

<style>
.hide {
  filter: blur(5px);
}
.hide:hover {
  filter: blur(0px);
}
</style>
