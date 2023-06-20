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
        <span class="m-l">单位</span>
        <Select v-model="company" class='m-l' style="width:150px">
          <Option v-for="item in companyList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">车系代码</span>
        <Select v-model="car" class='m-l' style="width:150px">
          <Option v-for="item in carList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">车系名称</span>
        <Input v-model="carName" placeholder="车系名称" style="width: 148px;height: 30px;"/>
      </div>
      <div class="search-item">
        <span class="m-l">整车分类</span>
        <Select v-model="carType" class='m-l' style="width:150px">
          <Option v-for="item in carTypeList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">整车级别</span>
        <Select v-model="carLevel" class='m-l' style="width:150px">
          <Option v-for="item in carLevelList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">结构</span>
        <Select v-model="structure" class='m-l' style="width:150px">
          <Option v-for="item in structureList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">在研项目号</span>
        <Input v-model="Num" placeholder="车系名称" style="width: 148px;height: 30px;"/>
      </div>
  	</div>
  	<Table highlight-row border :columns="columns" :data="data" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  </section>
</template>
<script>
export default{
	data(){
		return{
			car: '',
			carList: [],
			company:'',
			companyList: [],
			carName: '',
			carType: '',
			carTypeList: [],
			carLevel: '',
			carLevelList: [],
			structure: '',
			structureList: [],
			Num: '',
			columns: [
							{title: 'id',key: 'id',width: '70px'},
							{title: '单位代码',key: 'CarseriesCode'},
              {title: '单位名称',key: 'Carseriesname'},
              {title: '车系代码',key: 'Cartypecode'},
              {title: '生产工厂',key: 'Cartypename'},
              {title: '发动机类型',key: 'EngineCode'},
              {title: '上市时间',key: 'BoxCode'},
              {title: '在研项目号',key: 'ReportFlag'},
              {title: '在研项目名称',key: 'ShowFlag'},
              {title: '整车分类',key: 'Maincartypeflag'},
              {title: '整车级别',key: 'DriveWay'},
              {title: '结构',key: 'Seats'},
              {title: '能源',key: 'ShowCarCode'},
              {title: '产能(万辆/年)',key: 'ShowCarName'},
              {title: '退市时间',key: 'StopFlag'},
              {title: '退市标识',key: 'StopDate'}],
	    data: [
		        {
		        		id: '1001',
		            CarseriesCode: '1005',
		            Carseriesname: '奔腾450',
		            Cartypecode: '1.6',
		            Cartypename: '奔腾',
		            EngineCode: 'B502',
		            BoxCode: '1.6L',
		            ReportFlag: '1',
		            ShowFlag: '奔腾450',
		            Maincartypeflag: 'B502',
		            DriveWay: '1.6L',
		            Seats: '1.6L',
		            ShowCarCode: '1005',
		            ShowCarName: '奔腾450',
		            StopFlag: 'B502',
		            StopDate: '1.6L'
		        }]
			}
	},
	methods :{
		search(){
			console.log('查询')
//			var date = {
//	      unitCode: '1239989159',
//	      yuanUnit: 'wanyuan',
//	      carUnit: 'liang'
//	    }
//  	this.$axios.post('http://localhost:8080/yf-project-base/pageB/b1', date).then(response => {
//  		console.log(response.data)
//  		this.list = response.data
//  	})
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
