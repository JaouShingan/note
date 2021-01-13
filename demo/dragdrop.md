```vue
<template>
	<div class="box">
		<button v-on:click="change">change</button>
		<transition-group class="list" name="list-name" tag="div" ref="area">
			<div
				class="item"
				v-for="(item, index) in list"
				:key="item"
				:data-index="index"
				@mousedown="mousedown"
			>
				{{ item }}
			</div>
		</transition-group>
	</div>
</template>
<script>
export default {
	data() {
		return {
			list: [
				1,
				2,
				3,
				4,
				5,
				6,
				7,
				8,
				9,
				0,
				11,
				12,
				13,
				14,
				15,
				16,
				17,
				18,
				19,
				10
			],
			nextNum: 10,
			ghost: null,
			mouseOffset: null,
			moveTarget: null,
			hoverTarget: null,
			eleRect: []
		};
	},
	methods: {
		change() {
			var a = this.list.splice(2, 1);
			this.list.splice(6, 0, ...a);
		},
		setPosition(e) {
			this.ghost.style.left = e.clientX - this.mouseOffset.x + 'px';
			this.ghost.style.top = e.clientY - this.mouseOffset.y + 'px';
		},
		mousemove(e) {
			this.setPosition(e);
			const ele = this.eleRect.find((ele) => {
				console.log(ele, e.clientX, e.clientY);
				return (
					ele.x < e.clientX &&
					ele.y < e.clientY &&
					ele.x + ele.width > e.clientX &&
					ele.y + ele.height > e.clientY
				);
			});
			console.log(ele);
			if (ele) {
				this.hoverTarget = ele.index;
			}
		},
		mousedown(e) {
			const element = e.currentTarget;
			this.moveTarget = +element.dataset.index;
			const rect = element.getBoundingClientRect();
			this.mouseOffset = { x: e.offsetX, y: e.offsetY };
			this.ghost = element.cloneNode(true);
			this.ghost.style.width = rect.width + 'px';
			this.ghost.style.height = rect.height + 'px';
			this.ghost.style.position = 'fixed';
			this.setPosition(e);

			const arr = document.getElementsByClassName('item');
			const eleRect = [];
			for (let i = 0; i < arr.length; i++) {
				const r = arr[i].getBoundingClientRect();
				eleRect.push({
					width: r.width,
					height: r.height,
					x: r.x,
					y: r.y,
					index: arr[i].dataset.index
				});
			}
			console.log(eleRect);
			this.eleRect = eleRect;
			document.body.appendChild(this.ghost);
			document.body.addEventListener('mousemove', this.mousemove);
			document.body.addEventListener('mouseup', this.mouseup);
		},
		mouseup(e) {
			if (this.hoverTarget) {
				if (this.moveTarget < this.hoverTarget) {
					const [move] = this.list.splice(this.moveTarget, 1);
					this.list.splice(this.hoverTarget - 1, 0, move);
				} else if (this.moveTarget > this.hoverTarget) {
					const [move] = this.list.splice(this.moveTarget, 1);
					this.list.splice(this.hoverTarget, 0, move);
				}
			}
			console.log(this.list);
			this.ghost.remove();
			const arr = document.getElementsByClassName('item');
			for (let i = 0; i < arr.length; i++) {}
			document.body.removeEventListener('mousemove', this.mousemove);
			document.body.removeEventListener('mouseup', this.mouseup);
		},
		mouseenter(e) {
			this.hoverTarget = +e.currentTarget.dataset['index'];
		},
		mouseleave(e) {
			this.hoverTarget = null;
		}
	}
};
</script>
<style lang="less" scoped>
.box {
	// height: 150px;
	// overflow: scroll;
}
.list {
	width: 200px;
	display: grid;
	grid-template-columns: repeat(4, auto);
	grid-gap: 20px;
	.item {
		text-align: center;
		border: 1px solid black;
	}
}
.item {
	text-align: center;
	border: 1px solid black;
}
.list-name-move {
	transition: all 1s;
}
</style>
```
