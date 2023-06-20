<template>
  <section>
  	<div class="search">
  		<div class="search-button">
	  		<Button type="default" size="large"@click="add()">新增</Button>
	  		<Button type="default" size="large"@click="Delete()">删除</Button>
	  		<Button type="default" size="large" @click="modify()">修改</Button>
  		</div>
  	</div>
  	<Table highlight-row border :columns="columns" :data="data" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  </section>
</template>
<script>
export default{
	data(){
		return{
			columns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '顺序号',key: 'Seq'},
              {title: '节点代码',key: 'ItemNode'},
              {title: '节点名称',key: 'ItemNodeName'},
              {title: '周期(月)',key: 'CarNodePeriod'},
              {title: '停用标识',key: 'IsStop'},
              {title: '停用时间',key: 'StopDate'}],
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
	methods :{
		add(){
			console.log('添加')
		},
		getRow(){
			
		},
		Delete(){
			console.log('删除')
		},
		modify(){
			console.log('修改')
		}
	},
  mounted(){
	}
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
