<template>
	<view>
		<view class="html2canvas" :prop="domId" :change:prop="html2canvas.create">
			<slot></slot>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'html2canvas',
		props: {
			domId: {
				type: String,
				required: true
			}
		},
		methods: {
			async renderFinish(base64) {
				try{
					this.$emit('renderFinish', base64);
				}catch(e){
					//TODO handle the exception
					console.log('html2canvas error', e)
				}
			},
			showLoading() {
				uni.showToast({
					title: "正在生成海报",
					icon: "none",
					mask: true,
					duration: 100000
				})
			},
			hideLoading() {
				uni.hideToast();
			}
		}
	}
</script>



<script module="html2canvas" lang="renderjs">
import html2canvas from 'html2canvas';
export default {
	methods: {
		async create(domId) {
			try {
				this.$ownerInstance.callMethod('showLoading', true);
				const timeout = setTimeout(async ()=> {
					const shareContent = document.querySelector(domId);
					const canvas = await html2canvas(shareContent,{
						width: shareContent.offsetWidth,//设置canvas尺寸与所截图尺寸相同，防止白边
						height: shareContent.offsetHeight,//防止白边
						logging: true,
						useCORS: true
					});
					const base64 = canvas.toDataURL('image/jpeg', 1);
					this.$ownerInstance.callMethod('renderFinish', base64);
					this.$ownerInstance.callMethod('hideLoading', true);
					clearTimeout(timeout);
				}, 500);
			} catch(error){
				console.log(error)
			}
		}
	}
}
</script>


<style lang="scss">

</style>
