<template>

  <div class="widgetShowSession">
    <div class="title level1">Wizard</div>
    <div class="describe">
      Wizard控件是一个向导控件，用于描述一个流程，能够清晰看到流程进行到哪一个步。
    </div>

    <div class="showArea">
      <marvel-tab :tabItems="tabItems1">
        <marvel-tab-item :isActive="tabItems1[0].isActive">
          <div class="showAreaInner">
            <!--2级DemoView start-->
            <div>
              <button v-on:click="setProgress">setProgress</button>
              <marvel-wizard ref="ref0" :items="items"></marvel-wizard>
            </div>
            <!--2级DemoView end-->
          </div>
        </marvel-tab-item>
        <marvel-tab-item :isActive="tabItems1[1].isActive">
          <div class="codeArea">
            <!--2级CodeView start-->
              <pre v-highlight>
                <code class="html">
&lt;marvel-wizard ref="ref0" :items="items"&gt;&lt;/marvel-wizard&gt;
                </code>
              </pre>
            <!--2级CodeView end-->
          </div>
        </marvel-tab-item>
      </marvel-tab>
    </div>
  </div>
</template>

<script>
  import MarvelWizard from "@/walle/widget/wizard/MarvelWizard";
  import MarvelTab from "@/walle/widget/tab/MarvelTab";
  import MarvelTabItem from "@/walle/widget/tab/MarvelTabItem";

  export default {
    name: 'page4Wizard',
    components: {
      MarvelWizard,
      MarvelTab,
      MarvelTabItem
    },
    data: function() {
      return {
        tabItems1: [
          {
            label: "Demo View",
            isActive: true
          },
          {
            label: "Code View",
            isActive: false
          }
        ],
        items: [{
          label: "Basic Information",
          index: 1
        }, {
          label: "Condition",
          index: 2
        }, {
          label: "Action",
          index: 3
        }]
      }
    },
    methods: {
      setProgress: function(){
        this.$refs.ref0.setProgress(1);
        this.$refs.ref0.setProgress(2);
      }
    }
  }
</script>

<style scoped>

  .widgetShowSession {
    padding: 20px 100px;
    width: 100%;
    box-sizing: border-box;
  }

  .title {
    color: #4d4d4d;
  }

  .level1 {
    font-size: 32px;
    line-height: 54px;
  }

  .describe{
    font-size: 14px;
    color: #666;
    line-height: 36px;
  }

  .showArea {
    width: 100%;
    height: 400px;
  }

  .codeArea{
    width: 100%;
    height:100%;
    background-color: #f0f0f0;
    overflow: auto;
  }

  .codeArea pre,.codeArea code{
    padding: 0;
    margin: 0;
    min-width: 100%;
    float: left;
  }

  .showAreaInner {
    padding-top: 36px;
    box-sizing: border-box;
  }

  ::-webkit-scrollbar{
    width:8px;
    height:8px;
    background-color: rgba(0,0,0,0);
  }
  ::-webkit-scrollbar-track{
    border-radius: 10px;
    background-color: rgba(0,0,0,0);
  }
  ::-webkit-scrollbar-thumb{
    border-radius: 10px;
    background-color: rgba(0,0,0,0.4);
  }

</style>
