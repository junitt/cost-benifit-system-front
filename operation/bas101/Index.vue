<template>
	<section>
		<div class="search">
			<div class="search-button">
				<Button type="default" size="large" @click="add()">新增</Button>
				<Button type="default" size="large" @click="Delete()">删除</Button>
				<Button type="default" size="large" @click="modify()">修改</Button>
			</div>
		</div>
		<Table highlight-row border :columns="columns" :data="data" @on-row-dblclick="modify($event)"
			@on-row-click="getRow($event)"></Table>
		<div class="modal-mask" v-if="show">
			<div class="modal-wrap">
				<div class="modal">
					<div class="modal-content">
						<a class="modal-close" @click="cancel">
							<Icon type="ios-close" />
						</a>
						<div class="modal-header">{{ mdalTitel }}</div>
						<div class="modal-body">
							<Form class="modal-form" ref="formValidate" :model="formValidate" :label-width="85">
								<FormItem label="节点代码" prop="ItemNode" class="formItem">
									<Input v-model="formValidate.itemNode" placeholder="请填写节点代码"></Input>
								</FormItem>
								<FormItem label="节点名称" prop="ItemNodeName" class="formItem">
									<Input v-model="formValidate.itemNodeName" placeholder="请填写节点名称"></Input>
								</FormItem>
								<FormItem label="周期(月)" prop="CarNodePeriod" class="formItem">
									<Input v-model="formValidate.carNodePeriod" placeholder="请填写周期(月)"></Input>
								</FormItem>
								<FormItem label="停用标识" prop="IsStop" class="formItem">
									<Input v-model="formValidate.isStop" placeholder="请填写停用标识"></Input>
								</FormItem>
								<FormItem label="停用时间" prop="StopDate" class="formItem">
									<Input v-model="formValidate.stopDate" placeholder="请填写停用时间"></Input>
								</FormItem>
							</Form>
						</div>
						<div class="modal-footer">
							<Button type="default" @click="cancel">取消</Button>
							<Button type="primary" @click="save">确定</Button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>
<script>
export default {
	data() {
		return {
			columns: [
				{ title: 'id', key: 'id', width: '70px' },
				{ title: '顺序号', key: 'seq' },
				{ title: '节点代码', key: 'itemNode' },
				{ title: '节点名称', key: 'itemNodeName' },
				{ title: '周期(月)', key: 'carNodePeriod' },
				{ title: '停用标识', key: 'isStop' },
				{ title: '停用时间', key: 'stopDate' }],
			formValidate: {
				itemNode: '',
				itemNodeName: '',
				carNodePeriod: '',
				isStop: '',
				stopDate: ''
			},
			show: false,
			mdalTitel: '新增',
			data: [
				{
					id: '1001',
					Seq: '1005',
					ItemNode: '奔腾450',
					ItemNodeName: 'B502',
					CarNodePeriod: '1.6L',
					IsStop: '1005',
					StopDate: '奔腾450'
				}]
		}
	},
	methods: {
		//search更新数据
		search() {
			//网址李书记来写
			//空对象{}作为空的数据提交
			// response.data: {
			// 	date:[{
			// 		id: '1001',
			// 		Seq: '1005',
			// 		ItemNode: '奔腾450',
			// 		ItemNodeName: 'B502',
			// 		CarNodePeriod: '1.6L',
			// 		IsStop: '1005',
			// 		StopDate: '奔腾450'
			// 	}...
			// 	]
			// }
			this.$axios.post('http://localhost:8080/yf-project-base/node/list', {}).then(response => {
				this.data = response.data.date
				console.log(response.data)
			})
		},
		cancel() {
			this.show = false
		},
		add() {
			this.mdalTitel = '新增'
			this.formValidate.itemNode = 'a'
			this.formValidate.itemNodeName = 'b'
			this.formValidate.carNodePeriod = 'c'
			this.formValidate.isStop = 'd'
			this.formValidate.stopDate = ''
			this.show = true
		},
		getRow(data) {
			this.rowData = data
			console.log(this.rowData)
		},


		//写
		Delete() {
			var date = [{ id: this.rowData.id }]
			console.log(date)
			//路由交给李书记自己编
			//输入：当前行的id
			//返回：data
			this.$axios.post('http://localhost:8080/yf-project-base/node/remove', date).then(response => {
				this.search()
				this.$Message.info('删除成功')
			})
		},


		//写
		save() {
			console.log(this.formValidate)
			console.log(this.formValidate.ItemNode)
			if (true) {
				//formValidate: {ItemNode: '',  ItemNodeName: '',  CarNodePeriod: '',   IsStop: '',  StopDate: '' },
				//data
        console.log("hello")
				this.$axios.post('http://localhost:8080/yf-project-base/node/add', this.formValidate).then(response => {
					this.search()
          console.log(response.data)
					this.$Message.info('保存成功')
				})
			} else {
        console.log("maige")
				var date = [this.formValidate]
				//将当前用户信息对象formValidate存储到名为date的数组中
				//data
				this.$axios.post('http://localhost:8080/yf-project-base/node/modify', date).then(response => {
					this.search()
					this.$Message.info('修改成功')
				})
			}
			this.show = false
		},
		modify() {
			this.mdalTitel = '修改'
			this.show = true
			this.formValidate = this.rowData
		}
	},
	mounted() {
		this.search()
	}
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
