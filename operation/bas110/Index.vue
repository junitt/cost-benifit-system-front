<template>
  <section>
  	<div class="search">
  		<div class="search-button">
	  		<Button type="default" size="large" @click="save()">修改</Button>
  		</div>
  		<div class="search-item">
  			<span>项目类型</span>
        <RadioGroup v-model="typeRadio">
          <Radio label="cost">
            <span>费用</span>
          </Radio>
          <Radio label="price">
            <span>价格</span>
          </Radio>
        </RadioGroup>
      </div>
  	</div>
  	<Table v-if="this.typeRadio=='cost'" highlight-row border :columns="costColumns" :data="costData" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  	<Table v-if="this.typeRadio=='price'" highlight-row border :columns="priceColumns" :data="priceData" @on-row-dblclick="modify($event)" @on-row-click="getRow($event)"></Table>
  </section>
</template>
<script>
export default{
	data(){
		return{
			typeRadio: 'cost',
			costColumns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '项目1',key: 'Item1'},
              {title: '分摊规则',key: 'ShareRules'}],
	    costData: [
	        		{
		        		id: '1001',
		            Item1: '1005',
		            ShareRules: '奔腾450'
	        }],
    	priceColumns: [
							{title: 'id',key: 'id',width: '70px'},
              {title: '项目1',key: 'Item1'},
              {title: '分摊规则',key: 'ShareRules'}],
	    priceData: [
	        		{
		        		id: '1002',
		            Item1: '促销费',
		            ShareRules: '绝对值分摊'
	        }]
		}
	},
	methods :{
		getRow(){
			
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
