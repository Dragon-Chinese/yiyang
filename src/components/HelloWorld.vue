<template>
  <div class="common-layout">
    <el-container>
      <!-- <el-aside>
        <el-menu
        default-active="1-1"
        class="el-menu-vertical-demo"
        @open="handleOpen"
        @close="handleClose"
      >
        <el-sub-menu index="1">
          <template #title>
            <el-icon><location /></el-icon>
            <span>热血航线后台系统</span>
          </template>
          <el-menu-item-group title="申请福利">
            <el-menu-item index="1-1">奖励申请</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="系统扶持">
            <el-menu-item index="1-3">申请列表</el-menu-item>
          </el-menu-item-group>
          <el-sub-menu index="1-4">
            <template #title>人员登记</template>
            <el-menu-item index="1-4-1">item one</el-menu-item>
          </el-sub-menu>
        </el-sub-menu>
        <el-menu-item index="2">
          <el-icon><icon-menu /></el-icon>
          <span>游戏标志</span>
        </el-menu-item>
        <el-menu-item index="3" >
          <el-icon><document /></el-icon>
          <span>游戏星空</span>
        </el-menu-item>
        <el-menu-item index="4">
          <el-icon><setting /></el-icon>
          <span>后台设置</span>
        </el-menu-item>
      </el-menu>
      </el-aside> -->
      <el-container>
        <el-header>
          <el-page-header >
    <template #content>
      <div class="flex items-center">
        <el-avatar
          :size="32"
          class="mr-3"
          src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"
        />
        <span class="text-large font-600 mr-3"> 航海王 </span>
        <span class="text-sm mr-2" style="color: var(--el-text-color-regular)">
          管理员系统
        </span>
        <!-- <el-tag>最高权限</el-tag> -->
      </div>
    </template>
    <template #extra>
      <div class="flex items-center">
        <el-button>登出</el-button>
        <el-button type="primary" class="ml-2">设置</el-button>
      </div>
    </template>
  </el-page-header>
        </el-header>
        <el-main>
          <el-form
            style="max-width: 600px"
            :model="sizeForm"
            label-width="auto"
            :label-position="labelPosition"
            :size="size"
          >
          <li class="li-form">
            <el-form-item label="抖音名称">
              <el-input v-model="sizeForm.name"   placeholder="请输入抖音名称"/>
            </el-form-item>
           
          </li>
            
          <li class="li-form">
            <el-form-item label="游戏角色名称">
              <el-input v-model="sizeForm.name2"  placeholder="请输入游戏名称" />
            </el-form-item>
            <el-form-item label="游戏区服" style="margin-left: 20px ;">
              <el-input value="全大区" />
            </el-form-item>
          </li>
           
            <el-form-item label="抽卡次数">
              <el-select
                v-model="sizeForm.region"
                placeholder="请选择抽卡次数"
              >
                <el-option label="100高抽" value="100" />
                <el-option label="200高抽" value="200" />
                <el-option label="500高抽" value="500" />
                <el-option label="1000高抽" value="1000" />
              </el-select>
            </el-form-item>
            <el-form-item label="发放 管饱时间">
              <el-col :span="11">
                <el-date-picker
                  v-model="sizeForm.date1"
                  type="date"
                  aria-label="Pick a date"
                  placeholder="请选择时间"
                  style="width: 100%"
                />
              </el-col>
            </el-form-item>
            <el-form-item label="是否发放UR自选卡">
              <el-radio-group v-model="sizeForm.type">
                <el-radio border value="Online" name="type">
                  发放
                </el-radio>
                <el-radio border value="Promotion" name="type">
                  不发放
                </el-radio>
              </el-radio-group>
            </el-form-item>
            <el-form-item label="是否发放全套CDK礼包码">
              <el-radio-group v-model="sizeForm.resource">
                <el-radio border value="Sponsor">发放</el-radio>
                <el-radio border value="Venue">不发放</el-radio>
              </el-radio-group>
            </el-form-item>
            <el-form-item >
              <el-button style="margin-left: 150px;" type="danger" @click="onSubmit">申请</el-button>
              <el-button>清空</el-button>
            </el-form-item>
  </el-form>

  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="date" label="发放时间" width="100" />
    <el-table-column prop="name" label="名称" width="100" />
    <el-table-column prop="address" label="发放内容" />
  </el-table>
        </el-main>
      </el-container>
    </el-container>

    <el-dialog
    v-model="dialogVisible"
    title="申请成功"
    width="500"
    :before-close="handleClose"
  >
    <span>申请账户：{{ sizeForm.name }}</span>
    <br />
    <br />
    <span>到账时间：{{ sizeForm.date1 }}</span>
    <br />
    <br />
    <span>申请内容：1000高抽，全套升级材料，礼包码，UR自选卡</span>
    <template #footer>
      <div class="dialog-footer">
        <el-button type="primary" @click="handleClose">
          关闭
        </el-button>
      </div>
    </template>
  </el-dialog>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import { ElMessage } from 'element-plus'
const size = ref('default')
const labelPosition = ref('top')
// const handleOpen = () => {

// }
const handleClose = () => {
  dialogVisible.value = false
  sizeForm.name = ''
  sizeForm.region = ''
  sizeForm.type = ''
  sizeForm.resource = ''
  sizeForm.name2 = ''
}
const dialogVisible = ref(false)


const tableData = reactive([
  {
    date: '2024-07-03',
    name: '大飞哥',
    address: '1000高抽，全套升级材料，礼包码，UR自选卡',
  },
])

const sizeForm = reactive({
  name: '',
  name2: '',
  region: '',
  type: '',
  date1: '2024-07-03',
  delivery: false,
  resource: ''
})

const onSubmit = () => {
  if(!sizeForm.name) {
    return ElMessage({
    message: '请输入完整的信息',
    grouping: true,
    type: 'error',
  })
  }

  dialogVisible.value = true

  tableData.push({
    date: '2024-07-03',
    name: sizeForm.name,
    address: '1000高抽，全套升级材料，礼包码，UR自选卡',
  })

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
 ::v-deep .el-page-header__left {
  margin-right: 0 !important;
}
.el-form {
  width: 400px;
}
.li-form {
  display: flex;
  list-style: none;
}
.el-menu-item-group {
  padding-left: 26px;
}
.el-header {
  width: 100%;
  align-items: center;
  padding-top: 10px;
  .el-page-header__header   {
    display: flex;
    align-items: center;
    justify-content: space-between;
    .el-page-header__content .items-center {
      display: flex;
      align-items: center;
      span {
        margin: 0 10px;
        &:nth-of-type(3) {
          margin-left: -9px;
        }
      }
    }
  }
}
.el-aside {
  width: 185px;
  .el-menu {
    z-index: -9999;
  }
}
.common-layout {
  height: 100%;
  .el-container {
    height: 100%;
  }
  /* width: ; */
}
.el-menu--vertical {
  height: 100%;
}

</style>
