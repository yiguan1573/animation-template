<template>
	<div class="user-manage">
		<div class="manage-search">
			<el-input
					size="mini"
			    placeholder="请输入内容"
					@keyup.enter.native="handleClick"
			    v-model="input">
					<i slot="prefix" class="el-input__icon el-icon-search" @click="handleClick"></i>
			</el-input>
		</div>
		<el-button type="primary" plain class="add-system-message" size="mini" @click="sendSystemMessage">发送系统消息</el-button>
		<el-table
			:data="tableData"
			stripe
			border
			style="width: 100%">
			<el-table-column
				prop="title"
				label="标题"
				width="180">
				<template slot-scope="scope">
					<span style="text-overflow: ellipsis;white-space: nowrap;">{{ scope.row.title }}</span>
				</template>
			</el-table-column>
			<el-table-column
				prop="content"
				label="正文">
				<template slot-scope="scope">
					<span style="text-overflow: ellipsis;white-space: nowrap;">{{ scope.row.content }}</span>
				</template>
			</el-table-column>
			<el-table-column
				prop="userName"
				label="发送人"
				width="180">
				<template slot-scope="scope">
					<span style="text-overflow: ellipsis;white-space: nowrap;">{{ scope.row.userName }}</span>
				</template>
			</el-table-column>
			<el-table-column
				prop="time"
				label="时间"
				width="180">
				<template slot-scope="scope">
					<span style="text-overflow: ellipsis;white-space: nowrap;">{{ scope.row.time }}</span>
				</template>
			</el-table-column>
			<el-table-column label="操作" width="144">
			      <template slot-scope="scope">
			        <el-button
			          size="mini"
			          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
			        <el-button
			          size="mini"
			          type="danger"
			          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
			      </template>
			    </el-table-column>
		</el-table>
		
		<div style="float: right;margin-top: 20px;">
			<el-pagination
			  background
			 :hide-on-single-page="true"
			 :page-size="12"
			  layout="prev, pager, next"
			  :total="1000">
			</el-pagination>
		</div>
		
		<el-dialog title="编辑系统消息" :visible.sync="dialogFormVisible" append-to-body width="30%" center>
		  <el-form label-position="left" label-width="80px" :model="formData">
		    <el-form-item label="标题">
		      <el-input v-model="formData.title"></el-input>
		    </el-form-item>
		    <el-form-item label="正文">
		      <el-input v-model="formData.content"></el-input>
		    </el-form-item>
		  </el-form>
		  <div slot="footer" class="dialog-footer">
		    <el-button @click="dialogFormVisible = false">取 消</el-button>
		    <el-button type="primary" @click="ensure">确 定</el-button>
		  </div>
		</el-dialog>
		
	</div>
</template>

<script>
	export default {
		name: '',
		components:{

		},
		data(){
			return {
				input:'',
				 tableData: [
					{id:1,title:"B币券到账通知",time:"2022年10月7日 23:42",content:"领取任务后发布首稿即可得积分奖励！任务时间结束后，可在【我的-创作首页-新手任务】领取奖励。快来领取你的新手任务吧~",userName:"亿观"},
					{id:2,title:"B币券到账通知",time:"2022年10月7日 23:42",content:"领取任务后发布首稿即可得积分奖励！任务时间结束后，可在【我的-创作首页-新手任务】领取奖励。快来领取你的新手任务吧~",userName:"亿观"},
				],
				formData:{id:2,title:"B币券到账通知",time:"2022年10月7日 23:42",content:"领取任务后发布首稿即可得积分奖励！任务时间结束后，可在【我的-创作首页-新手任务】领取奖励。快来领取你的新手任务吧~",userName:"亿观"},
				dialogFormVisible: false,
				//记录当前弹框是哪一行数据
				index:1
			}
		},
		methods: {
			handleEdit(index, row) {
				this.dialogFormVisible = true
				this.formData = row
				this.index = index
			},
			handleDelete(index, row) {
				console.log(index, row);
			},
			handleClick(){
				this.$message('这是一条消息提示');
			},
			ensure(){
				this.dialogFormVisible = false
				console.log(this.formData)
				console.log(this.formData.hasOwnProperty('id'))
			},
			sendSystemMessage(){
				this.dialogFormVisible = true
				this.formData = {}
			}
		}
	}
</script>

<style lang="scss" scoped>
.user-manage{
	padding-left: 30px;
	padding-right: 30px;
	.manage-search{
		float: right;
		margin-top: 20px;
		margin-bottom: 10px;
	}
	.add-system-message{
		float: right;
		margin-top: 20px;
		margin-bottom: 10px;
		margin-right: 10px;
	}
}
</style>