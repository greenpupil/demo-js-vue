<template>
  <div class="phyWrapper">
    <topo-panel ref="ref4MainTopo4Phy"
                v-on:onTreeNodeClick="onTreeNodeClick"
                v-bind:items="items"
                id4Topo="phyTopo"
                theme="dark"></topo-panel>
    <marvel-bottom-ext-panel
      theme="dark"
      height="300"
      show="true"
      canDrag="false">
      <div class="phyContent" slot="content">
        <phy-grid-panel ref="ref4PhyGridPanel"
                        v-on:onClickRow4Ne="onClickRow4Ne"
                        v-on:onClickRow4Fiber="onClickRow4Fiber"></phy-grid-panel>
      </div>
    </marvel-bottom-ext-panel>
  </div>
</template>

<script>
  import TopoPanel from '@/components/0.common/0.2.topo/TopoPanel';
  import PhyGridPanel from "@/components/0.common/0.1.resourcePanel/PhyGridPanel";
  import MarvelBottomExtPanel from "@/walle/widget/extPanel/MarvelBottomExtPanel";

  export default {
    components: {
      TopoPanel,
      PhyGridPanel,
      MarvelBottomExtPanel,
    },
    name: "Phy",
    data: function () {
      return {
        //#region const
        debug: true,
        //#endregion
        //#region toolbar
        items: [{
          id: 0,
          label: '拓扑还原',
          icon: 'icon-marvelIcon-30'
        },{
          id: 1,
          label: '添加',
          icon: 'icon-marvelIcon-31'
        }, {
          id: 2,
          label: '保存',
          icon: 'icon-marvelIcon-32'
        }, {
          id: 3,
          label: '重置',
          icon: 'icon-marvelIcon-33'
        }, {
          id: 4,
          label: '导出',
          icon: 'icon-download'
        }, {
          id: 5,
          label: '布局',
          icon: 'icon-marvelIcon-34'
        }, {
          id: 6,
          label: '设置',
          icon: 'icon-marvelIcon-35'
        }, {
          id: 7,
          label: '选中',
          icon: 'icon-marvelIcon-36'
        }, {
          id: 8,
          label: '最佳视图',
          icon: 'icon-marvelIcon-38'
        }, {
          id: 9,
          label: '过滤',
          icon: 'icon-marvelIcon-39'
        }, {
          id: 10,
          label: '全屏',
          icon: 'icon-marvelIcon-40'
        }, {
          id: 11,
          label: '显示流量',
          icon: 'icon-marvelIcon-42'
        }, {
          id: 12,
          label: '创建光纤',
          icon: 'icon-marvelIcon-44'
        }, {
          id: 13,
          label: '返回上层',
          icon: 'icon-marvelIcon-45'
        }]
        //#endregion
      };
    },
    mounted: function () {
      this._getPhyTopo();
      this.$refs.ref4PhyGridPanel.init();
    },
    methods: {
      _getPhyTopo: function () {
        var self = this;
        if (this.debug) {
          var oData4LeftArea = {
            id: "root",
            name: 'root',
            icon: "icon-address-book",
            children: [{
              id: 'nodeBase0',
              name: 'nodeBase0',
              icon: "icon-address-book",
            }, {
              id: 'nodeBase1',
              name: 'nodeBase1',
              icon: "icon-address-book"
            }, {
              id: 'nodeBase2',
              name: 'nodeBase2',
              icon: "icon-address-book"
            }]
          };
          this.$refs.ref4MainTopo4Phy.setData4LeftArea(oData4LeftArea);
          this._getTopoDataMock(function (oTopoData) {
            self.$refs.ref4MainTopo4Phy.initTopo(function () {
              self.$refs.ref4MainTopo4Phy.drawTopo(oTopoData);
            });
          });
        }
        else {
          //TODO:
        }
      },
      _getTopoDataMock: function (oAfterCallBack) {
        var oTopoData = {
          nodes: [],
          nodeGroups: [],
          links: []
        };
        //#region node

        //#region 光站点
        var arrNodeGroup = [];
        for (var i = 0; i < 2; i++) {
          var iX = Math.random() * 400;
          var iY = Math.random() * 200;
          var oNodeGroup = {
            id: "nodeGroup" + i,
            x: iX,
            y: iY,
            uiImgKey: "nodeGroup",
            uiImgKey4Expand: "nodeGroupExpand",
            uiLabel: "nodeGroup" + i,
            uiExpandNode: false,
            uiExpandNodeWidth: 200,
            uiExpandNodeHeight: 200,
            uiNode: true,
            children: [{
              id: "node" + i + "_1",
              x: 50,
              y: 50,
              uiImgKey: "node",
              uiLabel: "node" + i + "_1",
              uiNode: true
            }, {
              id: "node" + i + "_2",
              x: 100,
              y: 100,
              uiImgKey: "node",
              uiLabel: "node" + i + "_2",
              uiNode: true
            }]
          };
          arrNodeGroup.push(oNodeGroup);
        }
        oTopoData.nodeGroups = arrNodeGroup;
        //#endregion

        //#region 网元
        var arrNode = [];
        for (var i = 0; i < 2; i++) {
          var iX = Math.random() * 400;
          var iY = Math.random() * 200;
          var oNode = {
            id: "node" + i,
            x: iX,
            y: iY,
            uiImgKey: "node",
            uiLabel: "node" + i,
            uiNode: true
          };
          arrNode.push(oNode);
        }
        for (var i = 0; i < 3; i++) {
          var iX = Math.random() * 400;
          var iY = Math.random() * 200;
          var oNode = {
            id: "nodeBase" + i,
            x: iX,
            y: iY,
            uiImgKey: "node",
            uiLabel: "nodeBase" + i,
            uiNode: true
          };
          arrNode.push(oNode);
        }
        oTopoData.nodes = arrNode;
        //#endregion

        //#endregion

        //#region link
        var arrLink = [];
        //#region 网元与网元之间的单条链路
        for (var i = 0; i < 3; i++) {
          var oLink = {
            id: "link" + i,
            srcNodeId: "nodeBase0",
            dstNodeId: "nodeBase1",
            uiLabelL: "nodeBase0",
            uiLabelM: "link" + i,
            uiLabelR: "nodeBase1",
            uiLink: true,
            uiLinkColorKey: "linkType1",
            uiLinkWidth: 3,
            uiDash: [10, 5]
          };
          arrLink.push(oLink);
        }
        //#endregion

        //#region 网元与网元之间的捆绑链路
        for (var i = 0; i < 2; i++) {
          //oLink1和oLink2为一组
          var oLink1 = {
            id: "gLink" + i + "_" + i,
            srcNodeId: "nodeBase" + i,
            dstNodeId: "nodeBase" + (i + 1),
            uiLinkGroupId: "groupLink" + i + "_" + i,
            uiLink: true,
            uiLinkExpand: false,
            uiLabelL: "nodeBase" + i,
            uiLabelM: "link" + i,
            uiLabelR: "nodeBase" + (i + 1),
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          var oLink2 = {
            id: "gLink" + i + "_" + (i + 1),
            srcNodeId: "nodeBase" + i,
            dstNodeId: "nodeBase" + (i + 1),
            uiLinkGroupId: "groupLink" + i + "_" + i,
            uiLink: true,
            uiLinkExpand: false,
            uiLabelL: "nodeBase" + i,
            uiLabelM: "link" + i,
            uiLabelR: "nodeBase" + (i + 1),
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          //oLink3和oLink4为一组
          var oLink3 = {
            id: "gLink" + i + "_" + (i + 2),
            srcNodeId: "nodeBase" + i,
            dstNodeId: "nodeBase" + (i + 1),
            uiLinkGroupId: "groupLink" + i + "_" + (i + 1),
            uiLink: true,
            uiLinkExpand: false,
            uiLabelL: "nodeBase" + i,
            uiLabelM: "link" + i,
            uiLabelR: "nodeBase" + (i + 1),
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };

          var oLink4 = {
            id: "gLink" + i + "_" + (i + 3),
            srcNodeId: "nodeBase" + i,
            dstNodeId: "nodeBase" + (i + 1),
            uiLinkGroupId: "groupLink" + i + "_" + (i + 1),
            uiLink: true,
            uiLinkExpand: false,
            uiLabelL: "nodeBase" + i,
            uiLabelM: "link" + i,
            uiLabelR: "nodeBase" + (i + 1),
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };

          arrLink.push(oLink1);
          arrLink.push(oLink2);
          arrLink.push(oLink3);
          arrLink.push(oLink4);
        }
        //#endregion

        //#region 网元与光设备之间的捆绑链路
        for (var i = 100; i < 101; i++) {
          var oLink1 = {
            id: "gLink" + i + 0,
            srcNodeId: "nodeBase2",
            dstNodeId: "node1_1",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i + 0,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 0,
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          var oLink2 = {
            id: "gLink" + i + 1,
            srcNodeId: "nodeBase2",
            dstNodeId: "node1_1",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i + 1,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 0,
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          var oLink3 = {
            id: "gLink" + i + 2,
            srcNodeId: "nodeBase2",
            dstNodeId: "node1_2",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i + 2,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 1,
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };
          var oLink4 = {
            id: "gLink" + i + 3,
            srcNodeId: "nodeBase2",
            dstNodeId: "node1_2",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i + 3,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 1,
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };
          arrLink.push(oLink1);
          arrLink.push(oLink2);
          arrLink.push(oLink3);
          arrLink.push(oLink4);
        }
        //#endregion

        //#region 光设备与光设备之间的捆绑链路
        for (var i = 200; i < 201; i++) {
          var oLink1 = {
            id: "gLink" + i + 0,
            srcNodeId: "node0_1",
            dstNodeId: "node1_1",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 0,
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          var oLink2 = {
            id: "gLink" + i + 1,
            srcNodeId: "node0_1",
            dstNodeId: "node1_1",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 0,
            uiLinkColorKey: "linkType2",
            uiLinkWidth: 3
          };
          var oLink3 = {
            id: "gLink" + i + 2,
            srcNodeId: "node0_2",
            dstNodeId: "node1_2",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 1,
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };
          var oLink4 = {
            id: "gLink" + i + 3,
            srcNodeId: "node0_2",
            dstNodeId: "node1_2",
            uiLabelL: "nodeBase0",
            uiLabelM: "gLink" + i,
            uiLabelR: "nodeBase1",
            uiLinkExpand: false,
            uiLink: true,
            uiLinkGroupId: "groupLink" + i + 1,
            uiLinkColorKey: "linkType3",
            uiLinkWidth: 3
          };
          arrLink.push(oLink1);
          arrLink.push(oLink2);
          arrLink.push(oLink3);
          arrLink.push(oLink4);
        }
        //#endregion
        oTopoData.links = arrLink;
        //#endregion

        oAfterCallBack(oTopoData);
      },
      onTreeNodeClick: function (oTreeNode) {
        this._getDevPropsByDevId(oTreeNode.id);
      },
      _getDevPropsByDevId: function (oRow) {
        if (this.debug) {
          var oData4RightArea = [
            [{
              value: "搬迁状态",
              type: "text"
            },{
              value: oRow[8].value,
              type: "text"
            }],[{
              value: "高阶使用容量",
              type: "text"
            },{
              value: oRow[9].value,
              type: "text"
            }],[{
              value: "高阶交叉个数",
              type: "text"
            },{
              value: oRow[10].value,
              type: "text"
            }],[{
              value: "低阶使用容量",
              type: "text"
            },{
              value: oRow[11].value,
              type: "text"
            }],[{
              value: "低阶交叉个数",
              type: "text"
            },{
              value: oRow[12].value,
              type: "text"
            }],[{
              value: "低阶等效VC4容量",
              type: "text"
            },{
              value: "4",
              type: "text"
            }],[{
              value: "低阶等效VC4个数",
              type: "text"
            },{
              value: "5",
              type: "text"
            }],[{
              value: "网元ID",
              type: "text"
            },{
              value: oRow[1].value,//TODO:待修改表格控件后修改
              type: "text"
            }],[{
              value: "网元名称",
              type: "text"
            },{
              value:oRow[2].value,
              type: "text"
            }],[{
              value: "网元类型",
              type: "text"
            },{
              value: oRow[4].value,
              type: "text"
            }],[{
              value: "设备厂商",
              type: "text"
            },{
              value: oRow[5].value,
              type: "text"
            }],[{
              value: "子架类型",
              type: "text"
            },{
              value: oRow[6].value,
              type: "text"
            }],[{
              value: "时隙模式",
              type: "text"
            },{
              value: oRow[7].value,
              type: "text"
            }],[{
              value: "IP地址",
              type: "text"
            },{
              value: "-",
              type: "text"
            }],[{
              value: "版本号",
              type: "text"
            },{
              value: "-",
              type: "text"
            }],[{
              value: "领域",
              type: "text"
            },{
              value: oRow[3].value,
              type: "text"
            }]
            ]

          this.$refs.ref4MainTopo4Phy.setData4RightArea(oData4RightArea);
        }
        else {
          //TODO:
        }
      },
      _getLinkPropsByLinkId: function (oRow) {
        if (this.debug) {
          var strSrcNe = oRow[5].value;
          var strDstNe = oRow[7].value;
          var oData4RightArea = [
            [{
              value: "链路利用率",
              type: "text"
            },{
              value: oRow[8].value,
              type: "text"
            }],[{
              value: "光纤名称",
              type: "text"
            },{
              value: oRow[1].value,
              type: "text"
            }],[{
              value: "光纤级别",
              type: "text"
            },{
              value: oRow[2].value,
              type: "text"
            }],[{
              value: "光纤放向",
              type: "text"
            },{
              value: oRow[3].value,
              type: "text"
            }],[{
              value: "光纤长度",
              type: "text"
            },{
              value: oRow[10].value,
              type: "text"
            }],[{
              value: "源端网络类型",
              type: "text"
            },{
              value: "SDH",
              type: "text"
            }],[{
              value: "源网元ID",
              type: "text"
            },{
              value: oRow[4].value,
              type: "text"
            }],[{
              value: "源网元名称",
              type: "text"
            },{
              value: oRow[4].value,//TODO:待修改表格控件后修改
              type: "text"
            }],[{
              value: "源网元槽位",
              type: "text"
            },{
              value:strSrcNe.substring(strSrcNe.indexOf("-")),
              type: "text"
            }],[{
              value: "源单板名称",
              type: "text"
            },{
              value: strSrcNe.substring(strSrcNe.indexOf("-"),strSrcNe.lastIndexOf("-")),
              type: "text"
            }],[{
              value: "源端口",
              type: "text"
            },{
              value: strSrcNe.substring(strSrcNe.lastIndexOf("-"),strSrcNe.length),
              type: "text"
            }],[{
              value: "宿端网络类型",
              type: "text"
            },{
              value: "SDH",
              type: "text"
            }],[{
              value: "宿网元ID",
              type: "text"
            },{
              value: oRow[6].value,
              type: "text"
            }],[{
              value: "宿网元名称",
              type: "text"
            },{
              value: oRow[6].value,
              type: "text"
            }],[{
              value: "宿网元槽位",
              type: "text"
            },{
              value: strDstNe.substring(strDstNe.indexOf("-")),
              type: "text"
            }],[{
              value: "宿单板名称",
              type: "text"
            },{
              value: strDstNe.substring(strDstNe.indexOf("-"),strDstNe.lastIndexOf("-")),
              type: "text"
            }],[{
              value: "宿端口",
              type: "text"
            },{
              value: strDstNe.substring(strDstNe.lastIndexOf("-"),strDstNe.length),
              type: "text"
            }],[{
              value: "数据来源",
              type: "text"
            },{
              value: oRow[9].value,
              type: "text"
            }]
          ];
          this.$refs.ref4MainTopo4Phy.setData4RightArea(oData4RightArea);
        }
        else {
          //TODO:
        }
      },
      onClickRow4Ne: function (oRow) {
        this._getDevPropsByDevId(oRow);
        this.$refs.ref4MainTopo4Phy.selectNe(oRow[1].value);
      },
      onClickRow4Fiber: function (oRow) {
        this._getLinkPropsByLinkId(oRow);
        this.$refs.ref4MainTopo4Phy.selectLink(oRow[1].value);
      }
    }
  }
</script>

<style>
  .phyWrapper {
    width: 100%;
    height: 100%;
    position: relative;
    background-color: #272743;
  }
  .phyContent{
    height:100%;
  }
</style>
