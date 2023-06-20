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
		    				<Form class="modal-form" ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="85">
					        <FormItem label="单位代码" prop="Code" class="formItem">
					            <Input v-model="formValidate.Code" placeholder="请填写单位代码"></Input>
					        </FormItem>
					        <FormItem label="单位名称" prop="Name" class="formItem">
					            <Input v-model="formValidate.Name" placeholder="请填写单位名称"></Input>
					        </FormItem>
					        <FormItem label="发动机型号" prop="EngineCode" class="formItem">
					            <Input v-model="formValidate.EngineCode" placeholder="请填写发动机型号"></Input>
					        </FormItem>
					        <FormItem label="发动机物料号" prop="Enginemtlcode" class="formItem">
					            <Input v-model="formValidate.Enginemtlcode" placeholder="请填写发动机物料号"></Input>
					        </FormItem>
					        <FormItem label="发动机类型" prop="EngineType" class="formItem">
					            <Input v-model="formValidate.EngineType" placeholder="请填写发动机类型"></Input>
					        </FormItem>
					        
					        <FormItem label="排量(L)" prop="Displacement" class="formItem">
					            <Input v-model="formValidate.Displacement" placeholder="请填写变速器类型"></Input>
					        </FormItem>
					        <FormItem label="气缸数" prop="CylinderNumber" class="formItem">
					            <Input v-model="formValidate.CylinderNumber" placeholder="请填写气缸数"></Input>
					        </FormItem>
					        <FormItem label="排放标准" prop="standard" class="formItem">
					            <Input v-model="formValidate.standard" placeholder="请填写排放标准"></Input>
					        </FormItem>
					        <FormItem label="功率(KW)" prop="Power" class="formItem">
					            <Input v-model="formValidate.Power" placeholder="请填写功率(KW)"></Input>
					        </FormItem>
					        <FormItem label="升功率(KW)" prop="Risingpower" class="formItem">
					            <Input v-model="formValidate.Risingpower" placeholder="请填写升功率(KW)"></Input>
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
        Code: '',  // 单位代码
        Name: '',  // 单位名称
        Enginemtlcode: '',  // 发动机物料号
        EngineType: '',  // 发动机类型
        EngineCode: '',  // 发动机型号
        Displacement: '',  // 排量(L)
        CylinderNumber: '',  // 气缸数
        standard: '',  // 排放标准
        Power: '',  // 功率(KW)
        Risingpower: '',  //升功率(KW)
      },
      ruleValidate: {
        Code: [{ required: true, message: '单位代码不能为空', trigger: 'blur' }],
        Name: [{ required: true, message: '单位名称不能为空', trigger: 'blur' }],
        Enginemtlcode: [{ required: true, message: '发动机物料号不能为空', trigger: 'blur' }],
        EngineCode: [{ required: true, message: '发动机型号不能为空', trigger: 'blur' }],
        EngineType: [{ required: true, message: '发动机不能为空', trigger: 'blur' }],
      },
      mdalTitel: '新增',
			car: '',
			value: '',
			carList: [],
			company:'',
			companyList: [],
			carName: '',
			show: false,
			rowData: '',
			columns: [
							{title: 'id',key: 'id',width: '70px'},
							{title: '单位代码',key: 'Code'},
              {title: '单位名称',key: 'Name'},
              {title: '发动机型号',key: 'EngineCode'},
              {title: '发动机物料号',key: 'Enginemtlcode'},
              {title: '发动机类型',key: 'EngineType'},
              {title: '排量(L)',key: 'Displacement'},
              {title: '气缸数',key: 'CylinderNumber'},
              {title: '排放标准',key: 'standard'},
              {title: '功率(KW)',key: 'Power'},
              {title: '升功率(KW)',key: 'Risingpower'}],
    data: [
        {
        		id: '1001',
            Code: '1005',
            Name: '奔腾450',
            Enginemtlcode: '1.6',
            EngineType: '奔腾',
            EngineCode: 'B502',
            Displacement: '1.6L',
            CylinderNumber: '1',
            standard: '奔腾450',
            Power: 'B502',
            Risingpower: '1.6L'
        },
        {
        		id: '1002',
            Code: '1005',
            Name: '奔腾450',
            Enginemtlcode: '1.6',
            EngineType: '奔腾',
            EngineCode: 'B502',
            Displacement: '1.6L',
            CylinderNumber: '0',
            standard: '奔腾450',
            Power: 'B502',
            Risingpower: '1.6L'
        },
        {
        		id: '1003',
            Code: '1005',
            Name: '奔腾450',
            Enginemtlcode: '1.6',
            EngineType: '奔腾',
            EngineCode: 'B502',
            Displacement: '1.6L',
            CylinderNumber: '1',
            standard: '奔腾450',
            Power: 'B502',
            Risingpower: '1.6L'
        },
        {
        		id: '1004',
            Code: '1005',
            Name: '奔腾450',
            Enginemtlcode: '1.6',
            EngineType: '奔腾',
            EngineCode: 'B502',
            Displacement: '1.6L',
            CylinderNumber: '0',
            standard: '奔腾450',
            Power: 'B502',
            Risingpower: '1.6L'
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
			this.formValidate.Code = ''  // 单位代码
	    this.formValidate.Name = ''  // 单位名称
	    this.formValidate.Enginemtlcode = ''  // 发动机物料号
	    this.formValidate.EngineType = ''  // 发动机物料号
	    this.formValidate.EngineCode = ''  // 发动机类型
	    this.formValidate.Displacement = ''  // 排量(L)
	    this.formValidate.CylinderNumber = ''  // 气缸数
	    this.formValidate.standard = ''  // 排放标准
	    this.formValidate.Power = ''  // 功率(KW)
	    this.formValidate.Risingpower = ''  //升功率(KW)
			this.show = true
		},
		getRow(data){
			this.rowData = data
		},
		Delete(){
			this.$Message.info('删除成功')
		},
		save(){
			if(this.formValidate.Code == '' || this.formValidate.EngineType == '' || this.formValidate.Enginemtlcode == '' || this.formValidate.Name == '' || this.formValidate.EngineCode == '' || this.formValidate.EngineType == ''){
			
			}else{
				this.$Message.info('保存成功')
				this.show = false
			}
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
