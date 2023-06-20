<template>
  <section>
  	<div class="search">
  		<div class="search-button">
  			<Button type="default" size="large" @click="search()">查询</Button>
	  		<Button type="default" size="large"@click="add()">新增</Button>
	  		<Button type="default" size="large"@click="Delete()">删除</Button>
	  		<Button type="default" size="large" @click="modify()">修改</Button>
  		</div>
  		<div class="search-item">
        <RadioGroup v-model="Radio">
          <Radio label="major">
            <span>专业组</span>
          </Radio>
          <Radio label="sub">
            <span>子组</span>
          </Radio>
        </RadioGroup>
      </div>
  		<div class="search-item">
        <span class="m-l">系统</span>
        <Select v-model="system" class='m-l' style="width:150px">
          <Option v-for="item in systemList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
  	</div>
  	<Table v-if="this.Radio=='major'" highlight-row border :columns="majorColumns" :data="data" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  	<Table v-if="this.Radio=='sub'" highlight-row border :columns="subColumns" :data="data" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  </section>
</template>
<script>
export default{
	data(){
		return{
			Radio: 'major',
			system:'',
			systemList: [],
			majorColumns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '体系',key: 'GroupSystem'},
              {title: '顺序号',key: 'Seq'},
              {title: '专业组代码',key: 'GroupCode'},
              {title: '专业组名称',key: 'GroupName'},
              {title: '停用标识',key: 'IsStop'},
              {title: '停用时间',key: 'StopDate'}],
      subColumns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '体系',key: 'GroupSystem'},
              {title: '顺序号',key: 'Seq'},
              {title: '子组代码',key: 'GroupCode'},
              {title: '子组名称',key: 'GroupName'},
              {title: '停用标识',key: 'IsStop'},
              {title: '停用时间',key: 'StopDate'}],
	    data: [
	        		{
		        		id: '1001',
		            GroupSystem: '1005',
		            Seq: '奔腾450',
		            GroupCode: 'B502',
		            GroupName: '1.6L',
		            IsStop: '1005',
		            StopDate: '奔腾450'
	        }]
		}
	},
	methods :{
		search(){
			console.log('查询')
		},
		getRow(){
		},
		add(){
			console.log('添加')
		},
		Delete(){
			console.log('删除')
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
