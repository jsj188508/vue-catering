<template>
	<div>
		<button class="own-login__switch" @click.prevent="toEvaluate" style="z-index: 99;font-size:0.875rem;">评价</button>
		<x-header :left-options="{backText: ''}" ref="hb">订单详情</x-header>
		<scroller lock-x height="-45" @on-scroll="onScroll" ref="orderViewScroller">
			<div>
				<group title="配送信息">
					<cell :title="deliveryAddress.nameAndPhone" :inline-desc="deliveryAddress.address"></cell>
				</group>
				<group title="商品信息">
					<x-table :cell-bordered="false" style="background-color:#fff;">
						<thead>
							<tr>
								<th>菜名</th>
								<th>单价</th>
								<th>数量</th>
							</tr>
						</thead>
						<tbody>
							<tr v-for="ol in order.orderList">
								<td>{{ol.product.name}}</td>
								<td>&yen;{{ol.rebate}}</td>
								<td>x {{ol.num}}</td>
							</tr>
						</tbody>
					</x-table>
				</group>
			</div>
		</scroller>
	</div>
</template>

<script>
import XHeader from 'vux/src/components/x-header/index.vue'
import Scroller from 'vux/src/components/scroller/index.vue'
import Group from 'vux/src/components/group/index.vue'
import XInput from 'vux/src/components/x-input/index.vue'
import XTextarea from 'vux/src/components/x-textarea/index.vue'
import XTable from 'vux/src/components/x-table/index.vue'
import Datetime from 'vux/src/components/datetime/index.vue'
import Cell from 'vux/src/components/cell/index.vue'
import CellBox from 'vux/src/components/cell-box/index.vue'

export default {
	components: {
		XHeader,
		Scroller,
		Group,
		XInput,
		XTextarea,
		XTable,
		Datetime,
		Cell,
		CellBox
	},
	data() {
		return {
			order: {
			},
			deliveryAddress: {}
		}
	},
	created() {
		let jsonStr = window.sessionStorage.getItem('orderView');
		let o = JSON.parse(jsonStr);
		this.order = o;
		this.deliveryAddress = o.deliveryAddress;
		this.deliveryAddress.nameAndPhone = o.deliveryAddress.name + ' ' + o.deliveryAddress.phone;
	},
	mounted() {
	},
	methods: {
		onScroll(pos) {
			this.scrollTop = pos.top
		},
		toEvaluate() {
			this.$router.push({ path: '/evaluate' });
		}
	}
}
</script>
<style scoped>
.demo2-item {
	width: 1.6rem !important;
	height: 1.6rem !important;
	border: 2px solid #ccc;
	display: inline-block;
	border-radius: 50%;
	line-height: 1.2rem;
	text-align: center;
	font-size: 0.75rem;
	box-sizing: border-box;
}

.demo2-item-selected {
	border-color: #FF563C;
	background-color: #FF563C;
	color: #fff;
}

.vux-checker-box {
	position: absolute !important;
	width: 60% !important;
	right: 10% !important;
}
</style>