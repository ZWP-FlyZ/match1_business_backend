
<style>
  @import "../../assets/css/edit.css";

</style>
<template>
  <div class=" regisiterpage">
    <HistoryPath :historyPathTitle="historyPathTitle"></HistoryPath>
    <div class="heads xf-heads">
      <i class="el-icon-share xf-edit-icon"></i> 流程基本信息
    </div>
    <div class="items">
      <form  class="itemsform">
        <div class="item">
          <label class="nameid">流程名称: </label><input type="text" class="inputbox checkView gm-input" value="女装T-shirt商品发布" autocomplete="on" autofocus="autofocus">
        </div>
         <div class="item">
          <label class="nameid">流程KEY: </label> <input type="text" class="inputbox checkView gm-input"  value="121" autocomplete="on" >
        </div>
        <div class="item">
          <label class="nameid">流程节点数: </label> <input type="text" class="inputbox checkView gm-input"  value="10"  autocomplete="on" >
        </div>
        <div class="item">
          <label class="nameid">流程描述: </label><input type="text" class="inputbox checkView gm-input"  value ="发布商品"  autocomplete="on" >
        </div>
        <div class="item">
          <label class="nameid"> 流程分类: </label>

          <select class="inputbox checkView SelectList basic-select gm-input" >
            <option >商品发布</option>
            <option value='' >一级流程</option>
          </select>
        </div>

        <div class="item">
          <label class="nameid">开发人员: </label> <input type="text" class="inputbox checkView gm-input"  value="xxx"  autocomplete="on" >
        </div>
        <div class="item">
          <label class="nameid">开发日期: </label> <input type="date" class="inputbox checkView gm-input"  value="2017-05-13"  autocomplete="on" >
        </div>
      </form>
    </div>
    <div class="heads xf-heads">
      <i class="el-icon-picture xf-edit-icon"></i> 流程图形化表达
    </div>
    <div class="items">
      <div class="xf-process-style" >
       <ProcessImg class="xf-process-img" v-on:show="showContent"></ProcessImg>
       <el-tabs v-model="editableTabsValue2" type="card" closable @tab-remove="removeTab">
         <el-tab-pane class="xf-content-height" v-for="(item, index) in editableTabs2" :key="item.name" :label="item.title" :name="item.name" >
          <div v-if="isshowActiviti">
            <div class="heads xf-heads-half">
              <i class="el-icon-share xf-edit-icon"></i> 节点基本信息
            </div>
            <div class="items">
              <div  class="xf-yellow">
                <div class="item">
                  <label class="nameid">节点名称: </label>
                  <input type="text" class="inputbox checkView gm-edit-input"  value="选择类目" autocomplete="on" autofocus="autofocus" v-if="item.id==0" >
                  <input type="text" class="inputbox checkView gm-edit-input"  value="是否选择货品模板" autocomplete="on" autofocus="autofocus" v-if="item.id==1">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="获取货品模板" autocomplete="on" autofocus="autofocus" v-if="item.id==2">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="填写商品信息" autocomplete="on" autofocus="autofocus" v-if="item.id==3">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="审核" autocomplete="on" autofocus="autofocus" v-if="item.id==4">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="人工审核" autocomplete="on" autofocus="autofocus" v-if="item.id==6">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="机器审核" autocomplete="on" autofocus="autofocus" v-if="item.id==5">

                  <label class="nameid">节点类型: </label>
                  <input type="text" class="inputbox checkView gm-edit-input"  value="子活动"  autocomplete="on" v-if="item.id==0||item.id==2||item.id==3||item.id==5||item.id==6">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="网关"  autocomplete="on" v-if="item.id==1||item.id==4">
                  
                  <label class="nameid">节点描述: </label> 
                  <input type="text" class="inputbox checkView gm-edit-input"  value="选择类目" autocomplete="on" autofocus="autofocus" v-if="item.id==0">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="是否选择货品模板" autocomplete="on" autofocus="autofocus" v-if="item.id==1">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="获取货品模板" autocomplete="on" autofocus="autofocus" v-if="item.id==2">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="填写商品信息" autocomplete="on" autofocus="autofocus" v-if="item.id==3">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="审核" autocomplete="on" autofocus="autofocus" v-if="item.id==4">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="人工审核" autocomplete="on" autofocus="autofocus" v-if="item.id==6">
                  <input type="text" class="inputbox checkView gm-edit-input"  value="机器审核" autocomplete="on" autofocus="autofocus" v-if="item.id==5">
                </div> 
              </div>
            </div>
          <br />
          <div class="heads xf-heads-half" v-if="item.id==0||item.id==2||item.id==3||item.id==6">
            <i class="el-icon-document xf-edit-icon"></i> 关联页面模板
          </div>
          <div class="items" v-if="item.id==0||item.id==2||item.id==3||item.id==6">
          <form  class="xf-yellow">
            <span class="item">
              <label class="xf-name-fix" v-if="item.id==6">人工审核</label>
              <label class="xf-name-fix" v-if="item.id==0">选择类目</label>
              <label class="xf-name-fix" v-if="item.id==2">选择货品模板</label>
              <label class="xf-name-fix" v-if="item.id==3">填写商品信息</label>
            </span>
            <span class="item xf-mutiple-position" v-if="item.id==0||item.id==2||item.id==3||item.id==6">
              <label class="xf-name-fix">关联的页面模板：</label>
             <MutipleSelectDelete v-if="item.id==6" class="xf-mutipleselect-top-fix xf-mutiple-width" v-bind:optionsdata="multiple.originOptions" v-bind:selecteddata="multiple.selectedList" v-on:selected="multipleCallback" v-bind:preview="true"></MutipleSelectDelete>
             <MutipleSelectDelete v-if="item.id==0" class="xf-mutipleselect-top-fix xf-mutiple-width" v-bind:optionsdata="multiple.lms" v-bind:selecteddata="multiple.selectedlm" v-on:selected="multipleCallback"></MutipleSelectDelete>
             <MutipleSelectDelete v-if="item.id==2" class="xf-mutipleselect-top-fix xf-mutiple-width" v-bind:optionsdata="multiple.hps" v-bind:selecteddata="multiple.selectedhp" v-on:selected="multipleCallback"></MutipleSelectDelete>
             <MutipleSelectDelete v-if="item.id==3" class="xf-mutipleselect-top-fix xf-mutiple-width" v-bind:optionsdata="multiple.sps" v-bind:selecteddata="multiple.selectedsp" v-on:selected="multipleCallback"></MutipleSelectDelete>
            </span>
          </form>
          <br />

          <!-- 页面图片 -->
          <transition name="showImg">
          <div class="xf-precondition-box xf-precondition-box-fix-height" v-if="item.id==2">
            <div v-for="i in multiple.selectedhp">
              <img src="../../assets/img/pages1.png" />
            </div>
          </div>
          <div class="xf-precondition-box xf-precondition-box-fix-height" v-if="item.id==3">
            <div v-for="i in multiple.selectedsp">
              <img src="../../assets/img/pages1.png" />
            </div>
          </div>
          <div class="xf-precondition-box xf-precondition-box-fix-height" v-if="item.id==6">
            <div v-for="i in multiple.selectedList">
              <img src="../../assets/img/pages1.png" />
            </div>
          </div>
          <div class="xf-precondition-box xf-precondition-box-fix-height" v-if="item.id==0">
            <div v-for="i in multiple.selectedlm">
              <img src="../../assets/img/pages1.png" />
            </div>
          </div>
          </transition>
          <!-- class = "xf-go-edit-bzability" -->
          <button @click="pagePre('selectedlm')" class = "link-btn link-btn-default" v-if="(item.id==0)&&multiple.selectedlm.length!=0">去编辑业务能力</button>
          <button @click="pagePre('selectedhp')" class = "link-btn link-btn-default" v-if="item.id==2&&multiple.selectedhp.length!=0">去编辑业务能力</button>
          <button @click="pagePre('selectedsp')" class = "link-btn link-btn-default" v-if="item.id==3&&multiple.selectedsp.length!=0">去编辑业务能力</button>
          <button @click="pagePre('selectedList')" class = "link-btn link-btn-default" v-if="item.id==6&&multiple.selectedList.length!=0">去编辑业务能力</button>
          </div>
          <div class = "heads xf-heads-half" v-if="item.id==4">
            <i class="el-icon-d-arrow-left xf-edit-icon"></i> 节点前置条件
          </div>
          <div class="items xf-items-addBottom" v-if="item.id==4">
          <form class="xf-yellow">
          <br />
            <div class="item xf-item xf-item-fix" v-for="i in precount">
             <div style="width:13%">
               <el-select v-model="value1" filterable placeholder="请选择">
                  <el-option v-for="item in outPreOptions" :key="item.name" :label="item.name" :value="item.name"></el-option>
                </el-select>
             </div>
              <div style="width:65%">
                <span class="xf-span-fix">若等于</span>
                <el-select v-model="value2" filterable placeholder="请选择">
                  <el-option v-for="item in outPreCondition" :key="item.name" :label="item.name" :value="item.name"></el-option>
                </el-select>
              <span class="xf-span-fix">则执行 <b>机器审核</b> 活动; 
              否则执行 <b>人工审核</b> 活动</span>
              </div>
              <div style="width:13%">
                <el-select v-model="value3" filterable placeholder="请选择">
                  <el-option v-for="item in options" :key="item.value" :label="item.value" :value="item.value"></el-option>
                </el-select>
              </div>
              <div class="xf-predition-delete">
                <i class="el-icon-plus xf-edit-icon" @click="showAdvance(0)"></i>
                <i class="el-icon-minus xf-edit-icon" @click="hideAdvance(0)" v-if="i!=1"></i>
              </div>
            </div>
          </form>
          </div>
          <div class = "heads xf-heads-half" v-if="item.id==100">
            <i class="el-icon-d-arrow-right xf-edit-icon"></i> 页面模板前置条件
          </div>
          <div class="items xf-items-addBottom" v-if="item.id==100">
          <form class="xf-yellow">
          <br />
            <div class="item xf-item xf-item-fix" v-for="pagei in pagecount">
             <div style="width:13%">
               <el-select v-model="value4" filterable placeholder="请选择">
                  <el-option v-for="item in outPreOptions" :key="item.name" :label="item.name" :value="item.name"></el-option>
                </el-select>
             </div>
              <div style="width:65%">
                <span class="xf-span-fix">若等于</span>
                <el-select v-model="value5" filterable placeholder="请选择">
                  <el-option v-for="item in outPreCondition" :key="item.name" :label="item.name" :value="item.name"></el-option>
                </el-select>
              <span class="xf-span-fix">则呈现 <b>页面1</b> ; 
              否则呈现 <b>页面2</b> </span>
              </div>
              <div style="width:13%">
                <el-select v-model="value6" filterable placeholder="请选择">
                  <el-option v-for="item in options" :key="item.value" :label="item.value" :value="item.value"></el-option>
                </el-select>
              </div>
              <div class="xf-predition-delete">
                <i class="el-icon-plus xf-edit-icon" @click="showAdvance(1)"></i>
                <i class="el-icon-minus xf-edit-icon" @click="hideAdvance(1)" v-if="pagei!=1"></i>
              </div>
            </div>
          </form>
          </div>

          
          <div class="heads xf-heads-half">
            <i class="el-icon-date xf-edit-icon"></i> 配置项
          </div>

          </div>
         </el-tab-pane>
       </el-tabs>
        </map>
      </div>
    </div>
    <br/>
    <div class="bottom" >
      <div class="BZProcess-table" style="border:0;">
          <div class="BZ-edit">
            <router-link to="/cCprocess"  class="link-btn link-btn-blue">上一步</router-link>
            <router-link to="/publishIdentity" class="link-btn link-btn-blue">下一步</router-link>
          </div>
      </div>
    </div>
    <IMask :hide-mask.sync="hideMask"></IMask>
    <ProcessPre :hide-pre.sync="hidePre" :hide-mask.sync="hideMask" v-on:closePre="closePre" :message="message"></ProcessPre>
    <br/>
  </div>
</template>
<script>
    import MutipleSelectDelete from "../AA/MutipleSelectDelete"
    import SingleSelect from '../CC/SingleSelect'
    import ProcessImg from './ProcessImg'
    import HistoryPath from '../HistoryPath'
    import ProcessPre from '../CC/ProcessL1Pre'
    import IMask from "../Mask"

    export default{
      data(){
        return {
          historyPathTitle:'业务方：选择业务标 / 选择流程 / 配置流程',
          isshowActiviti:false,
          showwhat :'5',
          multiple: {
            originOptions: [],
            selectedList: [],
            lms:[],
            hps:[],
            sps:[],
            selectedlm:[],
            selectedhp:[],
            selectedsp:[]
          },
          single:{
            originOptions:[],
            selected: {}
          },
          nodeList:[
            {"imgUrl":"static/img/node1.png","nodeText":"互斥网关","className":"fa-node1"},
            {"imgUrl":"static/img/node2.png","nodeText":"并行网关","className":"fa-node2"},
            {"imgUrl":"static/img/node3.png","nodeText":"网关","className":"fa-node3"},
            {"imgUrl":"static/img/node4.png","nodeText":"子活动","className":"fa-node4"},
            {"imgUrl":"static/img/node5.png","nodeText":"连接线","className":"fa-node5"}
          ],
          editableTabsValue2: '0',
          editableTabs2: [],
          tabIndex: 0,
          //showadvance:true,
          precount:1,
          pagecount:1,
          outPreOptions:[],
          options:[
            {value:'无'},
            {value:'与'},
            {value:'或'}
          ],
          value1:'',
          value2:'',
          value3:'',
          value4:'',
          value5:'',
          value6:'',
          preview:true,
          hidePre:true,
          hideMask:true,
          message:'page'
        }
      },
      components:{MutipleSelectDelete,SingleSelect,ProcessImg,HistoryPath,IMask,ProcessPre},
      mounted:function(){
        this.$nextTick(function(){
          this.queryData();
        })
      },
      methods:{
        queryData:function(){
          var mySelf = this
          /*单选的*/
          mySelf.outPreCondition = [{"id":"1","name":"达尔文"},{"id":"2","name":"类型1"},{"id":"3","name":"类型2"},{"id":"4","name":"类型3"},{"id":"5","name":"类型4"},{"id":"6","name":"类型5"}];
          mySelf.single.selected = {"id":"1","name":"达尔文"}
          /*多选的*/
          /*this.$http.get("/api/getList").then(res=>{
            mySelf.outPreOptions = JSON.parse(res.body.data).result.outPreCondition;
            JSON.parse(res.body.data).result.pageList
          })*/          
          mySelf.outPreOptions = [{"id":"1","name":"商品类型"},
      {"id":"2","name":"目标节点时限"},
      {"id":"3","name":"是否首次进入该节点"},
      {"id":"4","name":"商家信用等级"},
      {"id":"5","name":"开店时间"},
      {"id":"6","name":"转化率"},
      {"id":"7","name":"违规记录"},
      {"id":"8","name":"销售记录"},
      {"id":"9","name":"是否是良心卖家"},
      {"id":"10","name":"知名品牌高危质检"},
      {"id":"11","name":"冲突管理规则"}]
          mySelf.multiple.originOptions = [{"id":"1","name":"人工审核页面1"},{"id":"2","name":"人工审核页面2"}]
          mySelf.multiple.selectedList = [{"id":"1","name":"人工审核页面1"}]
          
          mySelf.multiple.lms = [{"id":"lm1","name":"选择类目页面模板"}]
          mySelf.multiple.selectedlm = [{"id":"lm1","name":"选择类目页面模板"}]

          mySelf.multiple.hps = [{"id":"hp1","name":"选择货品模板页面"}]
          mySelf.multiple.selectedhp = [{"id":"hp1","name":"选择货品模板页面"}]

          mySelf.multiple.sps = [{"id":"sp1","name":"填写商品信息页面"}]
          mySelf.multiple.selectedsp = [{"id":"sp1","name":"填写商品信息页面"}]
        },
        singleCallback: function(data){
            this.single.selected = data;
            // console.log('父级元素调用singleCallback 选中的是' + JSON.stringify(data))
        },
        multipleCallback: function(data){
          this.multiple.selectedList = data;
        },
        showContent:function(i,name){
          this.editableTabsValue2 = i
          this.isshowActiviti=true
          this.showwhat=i
          this.addTab(i,name);
          this.$nextTick(function(){
            this.queryData();
          })
        },
        removeTab:function(targetName) {
          let tabs = this.editableTabs2;
          let activeName = this.editableTabsValue2;
          if (activeName === targetName) {
            tabs.forEach((tab, index) => {
              if (tab.name === targetName) {
                let nextTab = tabs[index + 1] || tabs[index - 1];
                  if (nextTab) {
                    activeName = nextTab.name;
                  }
              }
            });
          }
          this.editableTabsValue2 = activeName;
          this.editableTabs2 = tabs.filter(tab => tab.name !== targetName);
        },
        addTab:function(targetName,name) {
          let newTabName = ++this.tabIndex + '';
          let tabs = this.editableTabs2;
          var isAdd = true;
          tabs.forEach((tab, index) =>{
            if(tab.id == targetName){
              this.editableTabsValue2 = targetName;
              isAdd = false;
              this.editableTabsValue2 = tab.name;
            }
          })
          if(isAdd){
             this.editableTabs2.push({
               id: targetName,
               title: name,
               name: name,
               content: 'New'
            });
            this.editableTabsValue2 = name;
          }
        },
        showAdvance:function(i){
          if(i==0)
            this.precount++;
          else
            this.pagecount++;
          //this.showadvance = false;
        },
        hideAdvance:function(i){
          if(i==0)
            this.precount--;
          else
            this.pagecount--;
          //this.showadvance = true;
        },
        pagePre:function(str){
          var type = "this.multiple."+str+".length";
          var a = eval(type);
          if(a > 1){
            this.hidePre = !this.hidePre
            this.hideMask = !this.hideMask
          }else{
            this.$router.push("/cCEditPage");
          }
        },
        closePre:function(childData,i){
          this.hideMask = childData
          this.hidePre = childData
          if(i==1){
            this.$router.push("/cCEditPageTemplate");
          }
        },
      }
    }   
  </script>
  <style scoped>
  .xf-item-fix{display:flex;justify-content:flex-start;align-items:flex-start;margin-bottom:20px;}
  .xf-predition-delete{margin-left:15px;margin-top:2px;}
  .xf-precondition-box-fix-height{height:auto;border:1px solid transparent;}
  .xf-precondition-box-fix-height img{width:100%;}
  .xf-precondition-box-fix-height div{border:1px solid #f0f0f0;width:30%;margin-right:1.5%;}
  .showImg-enter-active, .showImg-leave-active {
    transition: opacity .5s
  }
  .showImg-enter, .showImg-leave-active {
    opacity: 0
  }
  </style>
<style> 
  .xf-item{width:100%;}
  .xf-edit-icon{color:#448bc7;cursor: pointer;}
  .xf-item span.xf-span-fix{margin:0.3%;}
  .xf-single-fix{display: inline-block;height:30px;}
  .xf-node-style{text-align:center;}
  .xf-node-ul li {
  float:left;
  width:14%;
  display: inline-block;
  position: relative;
  margin: 0 1em;
  font-size: 1.5em;
}
  .node-style{width:60%;}
  .node-style-fix{position: relative;top:20px}
  .xf-detailNode{display: inline-block;}
  .xf-tooltip {display: inline;position: relative;z-index: 999;}
  .xf-tooltip-content {
  position: absolute;
  z-index: 9999;
  width: 220px;
  height: 110px;
  padding-top: 25px;
  left: 70%;
  top:-150px;
  margin-left: -40px;
  bottom: 100%;
  border-radius: 2%;
  text-align: center;
  background: #fff;
  color: #47c9af;
  opacity: 0;
  margin-bottom: 20px;
  cursor: default;
  pointer-events: none;
  border-radius: 4px;
  box-shadow: 3px 3px 3px #eee;
  border:1px solid #eee;
}
.xf-tooltip-content i {
  opacity: 0;
}

.xf-tooltip:hover .xf-tooltip-content,
.xf-tooltip:hover .xf-tooltip-content i {
  opacity: 1;
}
.xf-tooltip-effect-1 .xf-tooltip-content {
  -webkit-transform: translate3d(0,10px,0) rotate3d(1,1,1,0);
  transform: translate3d(0,10px,0) rotate3d(1,1,1,0);
  -webkit-transform-origin: 70% 100%;
  transform-origin: 70% 100%;
  -webkit-transition: opacity 0.3s, -webkit-transform 0.3s;
  transition: opacity 0.3s, transform 0.3s;
}

.xf-tooltip-effect-1 .xf-tooltip-content i {
  -webkit-transform: scale3d(0,0,1);
  transform: scale3d(0,0,1);
  -webkit-transition: opacity 0.3s, -webkit-transform 0.3s;
  transition: opacity 0.3s, transform 0.3s;
}
.xf-tooltip:hover .xf-tooltip-content,
.xf-tooltip:hover .xf-tooltip-content i {
  pointer-events: auto;
  -webkit-transform: translate3d(0,0,0) scale3d(1,1,1);
  transform: translate3d(0,0,0) scale3d(1,1,1);
}

.xf-tooltip-effect-1:hover .xf-tooltip-content i {
  -webkit-transform: rotate3d(1,1,1,0);
  transform: rotate3d(1,1,1,0);
}
.xf-node-text{position: relative;top:110px;color:#ccc;font-style: normal;font-size:14px;}
/* Arrow */

.xf-tooltip-content::after {
  content: '';
  position: absolute;
  top: 100%;
  left: 50%;
  margin: -7px 0 0 -15px;
  width: 30px;
  height: 20px;
  background-size: 100%;
}
.fa{
    width: 160px;
    height: 120px;
    display: inline-block;
    position: relative
    
}
.fa-node1{top: -60px;left: 10px;background: url(../../assets/img/node1.png);}
.fa-node2{top: -60px;left: 10px;background: url(../../assets/img/node2.png);}
.fa-node3{top: -60px;left: 10px;background: url(../../assets/img/node3.png);}
.fa-node4{top: -60px;left: -15px;background: url(../../assets/img/node4.png);}
.fa-node5{width:300px;top: -60px;left: -30px;background: url(../../assets/img/node5.png);}
.node-top-fix{top:-100px;}
.xf-process-style{text-align: center}
  .SelectList{
    border-style:none;
    appearance:none;
  }
  /*::-webkit-datetime-edit-fields-wrapper { background-color: red; }*/
  ::-webkit-datetime-edit-text { color: #878787; padding: 0 .3em; }/*/的颜色*/
  ::-webkit-datetime-edit-year-field { color: #878787;font: 15px/1.62 Helvetica,Arial,sans-serif; }
  ::-webkit-datetime-edit-month-field { color: #878787; }
  ::-webkit-datetime-edit-day-field { color: #878787; }
  .grey-option{
    margin-bottom: 20px;
  }
  .cc-precondition-pre-des{float: left;}
  .cc-precondition-search{float: left;}
  .longname-cc{top:0;}
  .xf-mutipleselect-top-fix{top:3px;z-index:101px;}
  .xf-go-edit-bzability{font-size:14px;color:#f7ba2a;}
  .xf-process-img{width:95%;}
  /*wxfei*/
  .xf-mutiple-position{position: relative;}
  .xf-mutiple-width{width:500% !important;left: 131px;}
  .xf-heads{background:#fff;border:1px dashed #448bc7;border-radius: 0px}
  .xf-heads-half{background:#fff;border:1px dashed #448bc7;border-radius: 0px;border-top:0px;border-right:0px;}
  .xf-yellow{background: #fff;text-align: left;margin-left:2%;}
  /*.xf-yellow div{margin:0px;padding:0px;}*/
  .xf-items-addBottom{margin-bottom: 0px}
  .item .xf-name-fix{position: relative;top:6px;}
  .xf-content-height{margin-bottom: 100px;padding:20px;}
  .xf-el-icon-plus{position: relative;top:-15px;left:5%;margin-right:4px;}
  .basic-inputbox{width: 200px;}
  .basic-select{padding:7px 4px 2px;}
  .gm-input{width: 200px;position: relative;top: 4px;padding:0 4px;border-radius: 4px;}/*页面上方基本信息处的input框*/
  .checkView{border:1px solid transparent;}/*去边框*/
  .gm-edit-input{padding:0 4px;position: relative;top: 4px;border-radius: 4px;}/*配置信息和前置条件处的input框*/
</style>