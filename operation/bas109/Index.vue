<template>
  <section>
  	<div class="search">
  		<div class="search-button">
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
              {title: '排量下限(L)',key: 'Low'},
              {title: '排量上限(L)',key: 'Hight'},
              {title: '税率(%)',key: 'Rate'}],
	    data: [
	        		{
		        		id: '1001',
		            Low: '1005',
		            Hight: '奔腾450',
		            Rate: 'B502',
	        }]
		}
	},
	methods :{
		Delete(){
			console.log('删除')
		},
		getRow(){
			
		},
		modify(){
			console.log('保存')
		}
	},
  mounted(){
	}
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
