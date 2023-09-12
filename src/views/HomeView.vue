<template>
  <div>
    <el-table :data="items" border style="width: 100%">
      <el-table-column
          prop="yuwen"
          label="语文"
          width="180"
      ></el-table-column>
      <el-table-column
          prop="shuxue"
          label="数学"
          width="180"
      ></el-table-column>
      <el-table-column prop="yinyu" label="英语" width="180"></el-table-column>
      < <el-table-column>
      <el-button @click="openEditDialog">修改</el-button>
      <el-button @click="deleteItem">删除</el-button>
    </el-table-column>
    </el-table>

    <el-dialog
        title="提示"
        :visible.sync="centerDialogVisible"
        width="30%"
        center
    >
      <div>
        <label>语文：</label>
        <el-input size="mini" v-model="yuwen"></el-input>
      </div>
      <div>
        <label>数学：</label>
        <el-input size="mini" v-model="shuxue"></el-input>
      </div>
      <div>
        <label>英语：</label>
        <el-input size="mini" v-model="yinyu"></el-input>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取消</el-button>
        <el-button type="primary" @click="saveChanges">确定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items: [],
      centerDialogVisible: false,
      yuwen: 0,
      shuxue: 0,
      yinyu: 0,
      selectedItem: null, // 选中的数据项
    };
  },

  mounted() {
    this.select();
  },

  methods: {
    // 打开编辑对话框，并传递选中的数据
    openEditDialog(item) {
      this.selectedItem = item;
      this.yuwen = item.yuwen;
      this.shuxue = item.shuxue;
      this.yinyu = item.yinyu;
      this.centerDialogVisible = true;
    },

    // 删除数据项的方法
    deleteItem() {
      // 实现删除逻辑，你可以在这里使用axios发送删除请求
    },

    // 保存修改的方法
    saveChanges() {
      // 执行保存修改的逻辑，可以使用axios发送保存请求
      // 这里假设要修改的数据已经保存成功

      axios.post("")
      // 刷新数据
      this.select();

      // 关闭对话框
      this.centerDialogVisible = false;
    },

    // 获取数据的方法
    select() {
      axios
          .get('http://10.100.255.51:8080/sorce/select')
          .then((response) => {
            this.items = response.data;
            console.log(this.items);
          })
          .catch((error) => {
            console.error('Error fetching data:', error);
          });
    },
    update(){

    }
  },
};
</script>