<template>
	<div>
		<el-input class="qInput" @focus="show()" size="small" v-model="input" placeholder="请输入内容"></el-input>
		<div class="qBox" v-if="flag">
			<el-tree class="qTree" :data="data" :props="defaultProps" @click="value()" @node-click="handleNodeClick"></el-tree>
			<el-button class="qButton" type="success" @click="addValue()">添加</el-button>
			<div class="qRight">
				<ul>
					<li v-for="i in showVal">{{i}}</li>
				</ul>
			</div>
			<el-button class="qBtn" type="primary" @click="hide()">确定</el-button>
		</div>
	</div>
</template>

<script>
	
	export default{
		name: 'Ele',
		data() {
		    return {
		        input: '',
		        flag:false,
		        val : '',
		        showVal:[],
		        data: [{
		          label: '部门',
		          children: [{
		            label: '部门1'
		          }]
		        }, {
		          label: '人员',
		          children: [{
		            label: '人员1'
		          }]
		        }],
		        defaultProps: {
		          children: 'children',
		          label: 'label'
		        }
		    }
		},
		methods:{
			show(){
				this.flag = true
				if(this.input != ''){
					this.showVal = this.input.split(' , ')
					console.log(this.showVal)
				}
			},
			hide(){
				this.flag = false
				this.input = this.showVal.join(' , ')
				console.log(this.input)
			},
			handleNodeClick(e) {
	           this.val=e.label
	        },
			addValue(){
				if(this.val != ''){
					this.showVal.push(this.val)
				}
				this.val=''
			}
		}
	}
	
</script>

<style>
	li{
		list-style: none;
	}
	.qBox{
		width: 48%;
		border: 1px solid #000;
		position: absolute;
	    top: 50%;
	    left: 50%;
	    height: 240px;
	    margin-top: -120px;
	    margin-left: -24%;
	    display: flex;
	    justify-content:space-between;
	    align-items:flex-start
	}
	.qInput{
		width: 16%;
	}
	.qTree{
		width: 30%;
	}
	.qRight{
		width: 20%;
		height: 100%;
		border-left: 1px solid #000;
	}
	.qButton{
		width: 50px;
		padding:0;
		margin-top: 84px;
		border: 1px solid #ccc;
		background: #fff;
		color: #000;
	}
	.qBtn{
		width: 90px;
		height: 32px;
		text-align: center;
		padding:0;
		position: absolute;
		bottom: 5px;
		left: 40%;
		color: #fff;
		font-size: 16px;
		background: dodgerblue;
	}
</style>