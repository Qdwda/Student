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
      <el-table-column>
        <el-button  @click="centerDialogVisible = true">修改</el-button>
        <el-button>删除</el-button>
      </el-table-column>
    </el-table>

    <el-dialog
        title="提示"
        :visible.sync="centerDialogVisible"
        @update:visible="handleDialogUpdate"
        width="30%"
        center
        @close="handleDialogClose"
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
    <el-button @click="centerDialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
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
      yuwen:0,
      shuxue:0,
      yinyu:0
    };
  },

  mounted() {
    this.select();
  },

  methods: {
    handleDialogUpdate(value) {
      console.log('Dialog visibility changed:', value);
    },

    handleDialogClose() {
      // Reload the page when the dialog is closed
      window.location.reload();
    },

    select() {
      axios
          .get('http://localhost:8080/sorce/select')
          .then((response) => {
            this.items = response.data;
            console.log(this.items);
          })
          .catch((error) => {
            console.error('Error fetching data:', error);
          });
    },
  },
};
</script>

