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
        <span class="m-l">工厂</span>
        <Select v-model="palntname" class='m-l' style="width:150px">
          <Option v-for="item in palntnameList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
  	</div>
    <Table highlight-row border :columns="columns" :data="data" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
    	<div class="modal-mask" v-if="show">
    		<div class="modal-wrap">
    			<div class="modal">
    				<div class="modal-content">
    					<a class="modal-close" @click="cancel"><Icon type="ios-close" /></a>
    					<div class="modal-header">{{mdalTitel}}</div>
    					<div class="modal-body">
		    				<Form class="modal-form" ref="formValidate" :model="formValidate" :label-width="85">
					        <FormItem label="工厂代码" prop="palntcode" class="formItem">
					            <Input v-model="formValidate.palntcode" placeholder="请填写发工厂代码"></Input>
					        </FormItem>
					        <FormItem label="工厂名称" prop="palntname" class="formItem">
					            <Input v-model="formValidate.palntname" placeholder="请填写工厂名称"></Input>
					        </FormItem>
					        <FormItem label="车间代码" prop="WorkShopCode" class="formItem">
					            <Input v-model="formValidate.WorkShopCode" placeholder="请填写单位代码"></Input>
					        </FormItem>
					        <FormItem label="车间名称" prop="WorkShopName" class="formItem">
					            <Input v-model="formValidate.WorkShopName" placeholder="请填写单位名称"></Input>
					        </FormItem>
					        <FormItem label="生产纲领" prop="Capacity" class="formItem">
					            <Input v-model="formValidate.Capacity" placeholder="请填写生产纲领(万辆/年)"></Input>
					        </FormItem>
					        <FormItem label="HR系统代码" prop="HrSysCode" class="formItem">
					            <Input v-model="formValidate.HrSysCode" placeholder="请填写HR系统代码"></Input>
					        </FormItem>
					        <FormItem label="停用标识" prop="StopFlag" class="formItem">
					            <Input v-model="formValidate.StopFlag" placeholder="请填写HR系统代码"></Input>
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
export default{
	data(){
		return{
			formValidate: {
        WorkShopCode: '',  
        WorkShopName: '',  
        palntcode: '',  
        palntname: '',
        Location: '',
        Capacity: '',
        HrSysCode: '',
        StopFlag: '',
      },
      mdalTitel: '新增',
			company:'',
			companyList: [],
			palntname: '',
			palntnameList: '',
			show: false,
			rowData: '',
			columns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '工厂代码',key: 'palntcode'},
              {title: '工厂名称',key: 'palntname'},
              {title: '车间代码',key: 'WorkShopCode'},
              {title: '车间名称',key: 'WorkShopName'},
              {title: '位置',key: 'Location'},
              {title: '生产纲领',key: 'Capacity'},
              {title: 'HR系统代码',key: 'HrSysCode'},
							{title: '停用标识',key: 'StopFlag'}],
    data: [
        {
        		id: '1001',
            WorkShopCode: '1005',
            WorkShopName: '奔腾450',
            palntcode: 'B502',
            palntname: '1.6L',
            Location: '1005',
            Capacity: '奔腾450',
            HrSysCode: 'B502',
            StopFlag: 0,
        }]
    }
	},
	methods :{
    cancel () {
    	this.show = false
    },
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
		modify(){
			this.mdalTitel = '修改'
			this.show = true
			this.formValidate = this.rowData
		},
		add(){
			this.mdalTitel = '新增'
			this.formValidate.WorkShopCode = ''
	    this.formValidate.WorkShopName = ''
	    this.formValidate.palntcode = ''
	    this.formValidate.palntname = ''
	    this.formValidate.Location = ''
	    this.formValidate.Capacity = ''
	    this.formValidate.HrSysCode = ''
			this.show = true
		},
		getRow(data){
			this.rowData = data
			console.log(this.rowData)
		},
		Delete(){
			this.$Message.info('删除成功')
		},
		save(){
				this.$Message.info('保存成功')
				this.show = false
		},
		dbclick(date){
			console.log(date)
		}
	},
  mounted(){
	}
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
