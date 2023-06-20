<template>
  <section>
  	<div class="search">
  		<div class="search-button">
  			<Button type="default" size="large" @click="search()">查询</Button>
  		</div>
  		<div class="search-item">
        <span class="m-l">单位</span>
        <Select v-model="company" class='m-l' style="width:150px">
          <Option v-for="item in companyList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">项目</span>
        <Select v-model="item" class='m-l' style="width:150px">
          <Option v-for="item in itemList" :value="item.label" :key="item.label"></option>
        </Select>
      </div>
      <div class="search-item">
        <span class="m-l">归档标识</span>
        <Checkbox></Checkbox>
      </div>
  	</div>
    <Table highlight-row border :columns="columns0" :data="data0"></Table><br /><br /><br />
    <div class="search">
  		<div class="search-button">
	  		<Button type="default" size="large"@click="add()">新增</Button>
	  		<Button type="default" size="large" @click="modify()">修改</Button>
	  		<Button type="default" size="large"@click="Delete()">删除</Button>
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
				        <FormItem label="版本号" prop="code" class="formItem">
				            <Input v-model="formValidate.code" placeholder="请填写单位代码"></Input>
				        </FormItem>
				        <FormItem label="项目节点" prop="name" class="formItem">
				            <Input v-model="formValidate.name" placeholder="请填写单位名称"></Input>
				        </FormItem>
				        <FormItem label="版本名称" prop="itemName" class="formItem">
				            <Input v-model="formValidate.itemName" placeholder="请填写发工厂代码"></Input>
				        </FormItem>
                <FormItem label="项目名称" prop="itName" class="formItem">
                  <Input v-model="formValidate.itName" placeholder="请填写项目名称"></Input>
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
  data () {
    return {
      formValidate: {
        code: '',
        name: '',
        itemName: '',
        itName: ''
      },
      mdalTitel: '新增',
      company: '',
      companyList: [],
      item: '',
      itemList: [],
      show: false,
      rowData: '',
      columns0: [
        {title: 'id', key: 'id', width: '70px'},
        {title: '单位代码', key: 'code'},
        {title: '单位名称', key: 'name'},
        {title: '项目名称', key: 'itemName'},
        {title: '项目类型', key: 'itemType'},
        {title: '对应车系', key: 'carseries'},
        {title: '归档标识', key: 'capacity'}],
      data0: [
        {
          id: '1001',
          code: '1005',
          name: '奔腾450',
          itemName: 'B502',
          itemType: '1.6L',
          carseries: '1005',
          capacity: 'B502'
        },
        {
          id: '1004',
          code: '1005',
          name: '奔腾450',
          itemName: 'B502',
          itemType: '1.6L',
          carseries: '1005',
          capacity: '奔腾450'
        }],
      columns: [
        {title: 'id', key: 'id', width: '70px'},
        {title: '版本号', key: 'unitId'},
        {title: '项目节点', key: 'unitName'},
        {title: '版本名称', key: 'plantName'},
        {title: '版本说明', key: 'planeCode'},
        {title: '是否正式版本', key: 'location'},
        {title: '创建日期', key: 'date'}],
      data: [
        {
          id: '1',
          unitId: '201703001',
          unitName: '项目前提',
          plantName: 'D015-项目前提-20170302',
          planeCode: '',
          location: '是',
          date: '2017/03/02'
        },
        {
          id: '1',
          unitId: '201703001',
          unitName: '项目前提',
          plantName: 'D015-项目前提-20170302',
          planeCode: '',
          location: '是',
          date: '2017/03/02'
        }]
    }
  },
  methods: {
    cancel () {
      this.show = false
    },
    // response.data: {
    //  date:[{
    //  id: '1001',
    //  code: '1005',
    //  name: '奔腾450',
    //  itemName: 'B502',
    //  itemType: '1.6L',
    //  carseries: '1005',
    //  capacity: 'B502'
    //  }...]
    // }
    search () {
      // date示例
      // date{
      // company:
      // item:
      // }
      let date = {
        company: this.company,
        item: this.item
      }
      this.$axios.post('http://localhost:8080/yf-project-base/itemversion/search', date).then(response => {
        console.log(response.data)
        this.data = response.data.date
      })
    },
    modify () {
      this.mdalTitel = '修改'
      this.show = true
      this.formValidate = this.rowData
    },
    add () {
      this.mdalTitel = '新增'
      this.formValidate.code = ''
      this.formValidate.name = ''
      this.formValidate.itemName = ''
      this.show = true
    },
    getRow (data) {
      this.rowData = data
      console.log(this.rowData)
    },
    Delete () {
      let date = {
        code: this.rowData.code
      }
      console.log(date)
      this.$axios.post('http://localhost:8080/yf-project-base/itemversion/remove', date).then(response => {
        this.search()
        this.$Message.info('删除成功')
      })
    },
    save () {
      console.log(this.formValidate)
      console.log(this.formValidate.code)
      let date = this.formValidate
      if (this.formValidate.code === '') {
        this.$axios.post('http://localhost:8080/yf-project-base/itemversion/add', date).then(response => {
          this.search()
          this.$Message.info('保存成功')
        })
      } else {
        this.$axios.post('http://localhost:8080/yf-project-base/itemversion/modify', date).then(response => {
          this.search()
          this.$Message.info('修改成功')
        })
      }
      this.show = false
    },
    getCompanyList () {
      console.log('getCompanyList')
      this.$axios.post('http://localhost:8080/yf-project-base/company/list', {}).then(response => {
        console.log(response.data)
        this.menuList = response.data.date
      })
    },
    getItemList () {
      console.log('getItemList')
      this.$axios.post('http://localhost:8080/yf-project-base/item/list', {}).then(response => {
        console.log(response.data)
        this.menuList = response.data.date
      })
    },
    mounted () {
      this.search()
      this.getCompanyList()
      this.getItemList()
    }
  }
}
</script>
<style lang="less" scoped>
@import '~@/assets/styles/base.less';
</style>
