<template>
  <div class="partPathArea">
    <div class="titleArea">
      <div class="titleName">不完整路径</div>
      <div class="btnArea">
        <marvel-icon-txt-button size="normal" classCustom="classCustom1"
                                label="导出"
                                icon="icon-download"
                                theme="dark"
                                v-on:onClick="onClick4ExportPartPath"></marvel-icon-txt-button>
        <marvel-icon-txt-button size="normal" classCustom="classCustom1"
                                label="网络删除"
                                icon="icon-bin"
                                theme="dark"
                                v-on:onClick="onClick4DelPartPath"></marvel-icon-txt-button>
        <marvel-icon-txt-button size="normal" classCustom="classCustom1"
                                label="删除"
                                icon="icon-bin"
                                theme="dark"
                                v-on:onClick="onClick4DelPartPathAndCross"></marvel-icon-txt-button>
      </div>
    </div>
    <div class="firstGridArea">
      <marvel-grid ref="ref4PartPathGrid"
                   :titles="titles4PartPath"
                   :rows="rows4PartPath"
                   :limit="limit4PartPath"
                   theme="dark"
                   v-on:onClickRow="onClickPartPathRow"></marvel-grid>
    </div>
    <div class="dynamicArea" v-show="showRouter">
      <div class="titleArea">
        <div class="titleName">路由详情</div>
        <div class="btnArea">
          <marvel-icon-txt-button size="normal" classCustom="classCustom1"
                                  label="导出"
                                  icon="icon-download"
                                  theme="dark"
                                  v-on:onClick="onClick4ExportRouter"></marvel-icon-txt-button>
        </div>
      </div>
      <div class="secondGridArea">
        <marvel-grid :titles="titles4PartRouter"
                     :rows="rows4PartRouter"
                     :limit="limit4PartRouter"
                     theme="dark"></marvel-grid>
      </div>
    </div>
  </div>
</template>

<script>
  import MarvelGrid from "@/walle/widget/grid/MarvelGrid";
  import MarvelIconTxtButton from "@/walle/widget/button/MarvelIconTxtButton";
  export default {
    components: {
      MarvelGrid,
      MarvelIconTxtButton
    },
    name: "PartPath",
    data: function () {
      return {
        //#region const
        debug: true,
        //#endregion
        //#region PartPathGrid
        titles4PartPath: [{
          label: "",
          width: "5%"
        }, {
          label: "业务名称",
          width: "13%"
        }, {
          label: "速率级别",
          width: "12%"
        }, {
          label: "方向",
          width: "8%"
        }, {
          label: "源网元名称",
          width: "10%"
        }, {
          label: "源槽位/单板/端口",
          width: "13%"
        }, {
          label: "源高阶时隙",
          width: "13%"
        }, {
          label: "源低阶时隙",
          width: "13%"
        }, {
          label: "宿网元名称",
          width: "10%"
        }, {
          label: "宿槽位/单板/端口",
          width: "13%"
        }, {
          label: "宿高阶时隙",
          width: "13%"
        }, {
          label: "宿低阶时隙",
          width: "13%"
        }, {
          label: "路径组Id",
          width: "10%"
        }, {
          label: "是否有保护",
          width: "13%"
        }, {
          label: "异常原因",
          width: "13%"
        }, {
          label: "建议处理方式",
          width: "13%"
        }],
        skip4PartPath: 0,
        limit4PartPath: 20,
        rows4PartPath: [],
        //#endregion
        //#region PartRouterGrid
        showRouter: false,
        titles4PartRouter: [{
          label: "",
          width: "5%"
        }, {
          label: "源网元名称",
          width: "13%"
        }, {
          label: "源槽位/单板/端口",
          width: "12%"
        }, {
          label: "源高阶时隙",
          width: "8%"
        }, {
          label: "源低阶时隙",
          width: "13%"
        }, {
          label: "宿网元名称",
          width: "10%"
        }, {
          label: "宿槽位/单板/端口",
          width: "13%"
        }, {
          label: "宿高阶时隙",
          width: "13%"
        }, {
          label: "宿低阶时隙",
          width: "13%"
        }, {
          label: "路由类型",
          width: "10%"
        }, {
          label: "资源类型",
          width: "13%"
        }, {
          label: "跳数",
          width: "13%"
        }, {
          label: "原业务名称",
          width: "13%"
        }],
        skip4PartRouter: 0,
        limit4PartRouter: 20,
        rows4PartRouter: [],
        //#endregion
      };
    },
    mounted: function () {
      if (this.debug) {
        this._getPartPathMock();
      }
      else {
        //TODO
      }
    },
    methods: {
      _getPartPathMock: function () {
        this.rows4PartPath = [];

        for (var i = 0; i < 10; i++) {
          var oRow = [{
            value: i + 1,
            type: "text"
          }, {
            value: "0001/E1_/CDMXDFCU/CDMXDFTP_" + i,
            type: "text"
          }, {
            value: "VC12",
            type: "text"
          }, {
            value: "单向",
            type: "text"
          }, {
            value: "nodeBase0",
            type: "text"
          }, {
            value: "8-SL16-" + i,
            type: "text"
          }, {
            value: i + 1,
            type: "text"
          }, {
            value: i + 1,
            type: "text"
          }, {
            value: "nodeBase2",
            type: "text"
          }, {
            value: "18-JQ16-" + i,
            type: "text"
          }, {
            value: i + 1,
            type: "text"
          }, {
            value: i + 1,
            type: "text"
          }, {
            value: "-",
            type: "text"
          }, {
            value: "否",
            type: "text"
          }, {
            value: "路径源或者宿未落地",
            type: "text"
          }, {
            value: "删除路由上的低阶业务",
            type: "text"
          }];
          this.rows4PartPath.push(oRow);
        }
      },
      _getPartRouterMock: function (oRow, oAfterCallback) {
        this.rows4PartRouter = [[{
          value: 1,
          type: "text"
        }, {
          value: oRow[5].value,
          type: "text"
        }, {
          value: oRow[6].value,
          type: "text"
        }, {
          value: oRow[7].value,
          type: "text"
        }, {
          value: oRow[8].value,
          type: "text"
        }, {
          value: oRow[5].value,
          type: "text"
        }, {
          value: oRow[6].value + 1,
          type: "text"
        }, {
          value: oRow[7].value + 1,
          type: "text"
        }, {
          value: oRow[8].value + 1,
          type: "text"
        }, {
          value: "正向工作",
          type: "text"
        }, {
          value: "VC12",
          type: "text"
        }, {
          value: "1",
          type: "text"
        }, {
          value: "",
          type: "text"
        }],[{
          value: 2,
          type: "text"
        }, {
          value: oRow[5].value,
          type: "text"
        }, {
          value: oRow[6].value+1,
          type: "text"
        }, {
          value: oRow[7].value+1,
          type: "text"
        }, {
          value: oRow[8].value+1,
          type: "text"
        }, {
          value: "nodeBase1",
          type: "text"
        }, {
          value: oRow[10].value,
          type: "text"
        }, {
          value: "-",
          type: "text"
        }, {
          value: "-",
          type: "text"
        }, {
          value: "正向工作",
          type: "text"
        }, {
          value: "Fiber",
          type: "text"
        }, {
          value: "2",
          type: "text"
        }, {
          value: "",
          type: "text"
        }],[{
          value: 3,
          type: "text"
        }, {
          value: "nodeBase1",
          type: "text"
        }, {
          value: oRow[10].value,
          type: "text"
        }, {
          value: oRow[11].value,
          type: "text"
        }, {
          value: oRow[12].value,
          type: "text"
        }, {
          value: "nodeBase1",
          type: "text"
        }, {
          value: oRow[10].value + 1,
          type: "text"
        }, {
          value: oRow[11].value + 1,
          type: "text"
        }, {
          value: oRow[12].value + 1,
          type: "text"
        }, {
          value: "正向工作",
          type: "text"
        }, {
          value: "VC12",
          type: "text"
        }, {
          value: "3",
          type: "text"
        }, {
          value: "",
          type: "text"
        }],[{
          value: 4,
          type: "text"
        }, {
          value: "nodeBase1",
          type: "text"
        }, {
          value: oRow[10].value+1,
          type: "text"
        }, {
          value: oRow[11].value+1,
          type: "text"
        }, {
          value: oRow[12].value+1,
          type: "text"
        }, {
          value: oRow[9].value,
          type: "text"
        }, {
          value: oRow[10].value + 2,
          type: "text"
        }, {
          value: "-",
          type: "text"
        }, {
          value: "-",
          type: "text"
        }, {
          value: "正向工作",
          type: "text"
        }, {
          value: "Fiber",
          type: "text"
        }, {
          value: "4",
          type: "text"
        }, {
          value: "",
          type: "text"
        }]];

        oAfterCallback(this.rows4PartRouter);
      },
      onClickPartPathRow: function (oRow) {
        var self = this;
        this.showRouter = true;
        if (this.debug) {
          this._getPartRouterMock(oRow, function (arrRouters) {
            self.$emit("onClickPartPathRow", arrRouters);
          });
        }
        else {
          //TODO:
        }
      },
      onClick4ExportRouter: function () {
        alert("onClick4ExportRouter");
      },
      onClick4ExportPartPath: function () {
        alert("onClick4ExportPartPath");
      },
      onClick4DelPartPath: function () {
        //获取勾选项
//        var arrCheckRows = this.$refs.ref4PartPathGrid.getCheckRows();
        alert("onClick4DelPartPath");
      },
      onClick4DelPartPathAndCross:function(){
        //获取勾选项
//        var arrCheckRows = this.$refs.ref4PartPathGrid.getCheckRows();
        alert("onClick4DelPartPathAndCross");
      }
    }
  }
</script>

<style scoped>
  .partPathArea{
    height:100%;
    width: 100%;
    overflow-y: auto;
    overflow-x: hidden;
  }
  .titleArea{
    width: 100%;
    height: 52px;
  }
  .titleName{
    float: left;
    height: 52px;
    font-size: 16px;
    color: #FFFFFF;
    /*font-weight: bold;*/
    line-height: 52px;
  }
  .btnArea{
    height: 52px;
    padding: 10px 0;
    box-sizing: border-box;
    float: right;
  }
  .firstGridArea{
    height: calc(100% - 52px);
  }
  .dynamicArea{
    padding-top: 20px;
    box-sizing: border-box;
  }
  .secondGridArea{
    height: 300px;
  }
  .classCustom1{
    margin-left: 20px;
  }
</style>
