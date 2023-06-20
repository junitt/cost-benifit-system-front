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
				        <FormItem label="项目代码" prop="ItemCode" class="formItem">
				            <Input v-model="formValidate.ItemCode" placeholder="请填写项目代码"></Input>
				        </FormItem>
				        <FormItem label="项目名称" prop="ItemName" class="formItem">
				            <Input v-model="formValidate.ItemName" placeholder="请填写项目名称"></Input>
				        </FormItem>
				        <FormItem label="项目类型" prop="ItemType" class="formItem">
				            <Input v-model="formValidate.ItemType" placeholder="请填写项目类型"></Input>
				        </FormItem>
				        <FormItem label="对应车系" prop="Carseries" class="formItem">
				            <Input v-model="formValidate.Carseries" placeholder="请填写对应车系"></Input>
				        </FormItem>
				        <FormItem label="项目说明" prop="ItemDocument" class="formItem">
				            <Input v-model="formValidate.ItemDocument" placeholder="请填写项目说明"></Input>
				        </FormItem>
				        <FormItem label="级别" prop="CarLevel" class="formItem">
				            <Input v-model="formValidate.CarLevel" placeholder="请填写级别"></Input>
				        </FormItem>
				        <FormItem label="结构" prop="CarClass" class="formItem">
				            <Input v-model="formValidate.CarClass" placeholder="请填写结构"></Input>
				        </FormItem>
				        <FormItem label="能源" prop="DriveType" class="formItem">
				            <Input v-model="formValidate.DriveType" placeholder="请填写能源"></Input>
				        </FormItem>
				        <FormItem label="尺寸（mm）" prop="Size" class="formItem">
				            <Input v-model="formValidate.Size" placeholder="请填写尺寸（mm）"></Input>
				        </FormItem>
				        <FormItem label="轴距（mm）" prop="WheelBase" class="formItem">
				            <Input v-model="formValidate.WheelBase" placeholder="请填写轴距（mm）"></Input>
				        </FormItem>
				        <FormItem label="归档标识" prop="ArchiveFlag" class="formItem">
				            <Input v-model="formValidate.ArchiveFlag" placeholder="请填写归档标识"></Input>
				        </FormItem>
				        <FormItem label="归档时间" prop="ArchiveDate" class="formItem">
				            <Input v-model="formValidate.ArchiveDate" placeholder="请填写归档时间"></Input>
				        </FormItem>
				        <FormItem label="图片" prop="BlobFile" class="formItem">
				            <Input v-model="formValidate.BlobFile" placeholder="请填写图片"></Input>
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
			company:'',
			companyList: [],
			formValidate: {
        ItemCode: '',  
        ItemName: '',  
        ItemType: '',
        Carseries: '',
        ItemDocument: '',
        CarLevel: '',
        CarClass: '',
        DriveType: '',
        Size: '',
        WheelBase: '',
        ArchiveFlag: '',
        ArchiveDate: '',
        BlobFile: ''
      },
      show: false,
      mdalTitel: '新增',
			columns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '单位代码',key: 'Code'},
              {title: '单位名称',key: 'Name'},
              {title: '项目名称',key: 'ItemName'},
              {title: '项目类型',key: 'ItemType'},
              {title: '对应车系',key: 'Carseries'},
              {title: '项目说明',key: 'ItemDocument'},
              {title: '整车分类',key: 'Type'},
							{title: '级别',key: 'CarLevel'},
							{title: '结构',key: 'CarClass'},
							{title: '能源',key: 'DriveType'},
							{title: '尺寸(mm)',key: 'Size'},
							{title: '轴距(mm)',key: 'WheelBase'},
							{title: '图片',key: 'BlobFile'},
							{title: '归档标识',key: 'ArchiveFlag'},
							{title: '归档时间',key: 'ArchiveDate'},
			],
	    data: [
	        		{
		        		id: '1001',
		            Code: '1005',
		            Name: '奔腾450',
		            ItemName: 'B502',
		            ItemType: '1.6L',
		            Carseries: '1005',
		            ItemDocument: '奔腾450',
		            Type: 'B502',
		            CarLevel: '奔腾450',
		            CarClass: 'B502',
		            DriveType: '1.6L',
		            Size: '1005',
		            WheelBase: '奔腾450',
		            BlobFile: '',
		            ArchiveFlag: '',
		            ArchiveDate: ''
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
			this.formValidate.ItemCode = ''
	    this.formValidate.ItemName = ''
	    this.formValidate.ItemType = ''
	    this.formValidate.Carseries = ''
	    this.formValidate.ItemDocument = ''
	    this.formValidate.CarLevel = ''
	    this.formValidate.CarClass = ''
	    this.formValidate.DriveType = ''
	    this.formValidate.Size = ''
	    this.formValidate.WheelBase = ''
	    this.formValidate.ArchiveFlag = ''
	    this.formValidate.ArchiveDate = ''
	    this.formValidate.BlobFile = ''
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
		}
	},
  mounted(){
	}
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
