<template>
	<div class="cars">
		<v-pageTitle>
			<span slot="title">车辆管理</span>
			<span slot="subTitle">车辆列表</span>
		</v-pageTitle>
		<div class="form-wrapper">
			<v-iform :fields="search.formModel" :inline="true"  ref="searchForm" :fieldData.sync='search.formData' @submitForm='_submit'>
				<div slot="iform-btns">
					<el-button type="success" size="small" @click="_valiDate">查询</el-button>
					<el-button type="default" size="small" @click="_reset">重置</el-button>
				</div>
			</v-iform>
		</div>
		<v-btnGroup>
			<el-button type="primary" size="small">导出</el-button>
		</v-btnGroup>
		<v-itable :tableModel="table.tableModel" border :tableData='table.tableData'></v-itable>
		<br>
		<div align="center">
			<el-pagination
		      @size-change="_handleSizeChange"
		      @current-change="_handleCurrentChange"
		      :current-page="pager.p"
		      :page-sizes="pager.sizes"
		      :page-size="pager.s"
		      layout="total, sizes, prev, pager, next, jumper"
		      :total="pager.total">
		    </el-pagination>
		</div>
		
	</div>
</template>

<script>
	import {cars_formModel,cars_tableModel} from 'base/api/resource/car.js'
	import iform from 'components/Forms/iform'
	import pageTitle from 'common/pageTitle'
	import btnGroup from 'common/btnGroup'
	import itable from 'components/table/itable'
	export default {
		name:'cars',
		data(){
			return {
				search:{
					formModel:cars_formModel,
					formData:{}
				},
				table:{
					tableModel:[
						{
							prop:'name',
							label:'车辆认证',
							width:120,
							render:(h,params) =>{
								return h('span',{
									class:{
										'link-type':true
									},
									on:{
										click:() =>{
											
										}
									}
								},'已认证');
							}
						}
					],
					tableData:[]
				},
				pager:{
					total:10,
					p:0,
					s:10,
					sizes:[10,20,40]
				}
			}
		},
		created(){
			this.table.tableModel = [...cars_tableModel,...this.table.tableModel,];
		},
		methods:{
			_submit(formData){
				console.log(formData);
			},
			_valiDate(){
				this.$refs.searchForm.valiDate();
			},
			_reset(){
				this.$refs.searchForm.$emit('resetForm');
			},
			_handleSizeChange(){
				
			},
			_handleCurrentChange(){
				
			}
		},
		components:{
			'v-pageTitle':pageTitle,
			'v-iform':iform,
			'v-btnGroup':btnGroup,
			'v-itable':itable
		}
	}
</script>

<style scoped lang="scss">
.form-wrapper{
	margin: 20px 0 0 0;
}
</style>