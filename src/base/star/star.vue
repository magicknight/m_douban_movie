<template>
	<div class="star" :class="starType">
		<span v-for="item in starClasses" class="star-item" :class="item"></span>
		<span class="average-font" v-if="needAverage">{{starTotal}}<span v-if="needRateTag">分</span></span>
		<span class="average-font text-gray" v-if="needWatched">{{watchedTotal}}人看过</span>
	</div>
</template>

<script>
	var LENGTH = 5;
	var CLS_ON = 'on';
	var CLS_HALF = 'half';
	var CLS_OFF = 'off';
	export default {
		props: {
			starTotal: {
				type: Number,
				default: 0
			},
			size: {
				type: Number,
				default: 24
			},
			needStar: {
				type: Boolean,
				default: true
			},
			needAverage: {
				type: Boolean,
				default: true
			},
			needRateTag: {
				type: Boolean,
				default: true
			},
			needWatched: {
				type: Boolean,
				default: false
			},
			watchedTotal: {
				type: Number,
			}
		},
		computed: {
			starType() {
				return 'star-' + this.size;
			},
			normalizaScore() {
				var star = this.starTotal.toString().length;
				if(star.length < 0){
					return '${star}.0'
				}else{
					return star
				}
			},
			starClasses() {
				var result  = [];
				var score = Math.floor(this.starTotal) / 2;
				var hasHalf = score % 1 !== 0;
				var integer = Math.floor(score);
				for(var i=0;i<integer;i++){
					result.push(CLS_ON);
				}
				if(hasHalf){
					result.push(CLS_HALF);
				}
				while(result.length < LENGTH){
					result.push(CLS_OFF);
				}
				return result;
			}
		}
	}
</script>

<style type="text/css">
	.star {
		text-align: left;
	}
	.star-24 .star-item {
		width: 50px;
		height: 50px;
		display: inline-block;
		margin-right: 20px;
		background-size: 50px 50px;
	}
	.star-24 .half {
		background-image: url('star24_half@2x.png');
	}
	.star-24 .on {
		background-image: url('star24_on@2x.png');
	}
	.star-24 .off {
		background-image: url('star24_off@2x.png');
	}
	.star-36 .star-item {
		width: 70px;
		height: 70px;
		display: inline-block;
		background-size: 10px 10px;
	}
	.star-36 .half {
		background-image: url('star36_on@2x.png');
	}
	.star-36 .on {
		background-image: url('star36_on@2x.png');
	}
	.star-36 .off {
		background-image: url('star36_off@2x.png');
	}
	.average-font {
		font-size: 0.8rem
	}
	.text-gray {
		color: #ccc;
	}
</style>