<template>
  <div id="editor">
    <nav>
      <ol>
        <li v-for="i in [0,1,2,3,4,5]" v-bind:class="{active: currentTab === i}" v-on:click="currentTab = i" >
          <svg class="icon">
            <use v-bind:xlink:href="`#icon-${icons[i]}`"></use>
          </svg>
        </li>
      </ol>
    </nav>
    <ol class="panes">
      <!--&lt;!&ndash;<li v-for="i in [0,1,2,3,4,5]" v-bind:class="{active: currentTab === i}" >-->
        <!--Tab {{i+1}}-->
      <!--</li>&ndash;&gt;-->
      <li v-bind:class="{active: currentTab === 0}">
        <profileEditor v-bind:profile="profile"/>
      </li>

      <li v-bind:class="{active: currentTab === 1}">
        <workHistoryEditor v-bind:workHistory="workHistory"/>
      </li>

      <li v-bind:class="{active: currentTab === 2}">
        <studyHistoryEditor v-bind:items="studyHistory"/>
      </li>
      <li v-bind:class="{active: currentTab === 3}">
        <h2>项目经历</h2>
      </li>
      <li v-bind:class="{active: currentTab === 4}">
        <h2>获奖情况</h2>
      </li>
      <li v-bind:class="{active: currentTab === 5}">
        <h2>联系方式</h2>
      </li>
    </ol>
  </div>
</template>

<script>
  import profileEditor from './profileEditor'
  import workHistoryEditor from './workHistoryEditor'
  import studyHistoryEditor from './studyHistoryEditor'
  export default {
      components:{ profileEditor,workHistoryEditor,studyHistoryEditor },
    data(){
      return {
        currentTab: 0,
        icons: ['shenfenzheng', 'work', 'book', 'heartsurgery', 'jiangbei', 'phone'],
        profile:{name:'',city:'',birth:''},
        workHistory:[{company:'',content:''}],
        studyHistory:[{school:'',duration:'',degree:''}]
      }
    },
    methods:{

    },
    created(){

    }
  }

</script>

<style lang="scss">
  #editor{ min-height: 100px;
    display: flex;
    > nav {
      background: #000;
      width: 80px;
      > ol > li {
        padding: 16px 0;
        text-align: center;
        > .icon {
          width: 24px;
          height: 24px;
          fill: white;
        }
        &.active{
          background: white;
          > .icon{
            fill: black;
          }
        }
      }
    }
    > .panes {
      flex:1;
        .container{
          position: relative;
          .el-icon-circle-close{
            position: absolute;
            right:0;top:0;
          }
        }
      > li{
        display: none;
        padding: 32px;
        overflow: auto;
        height:100%;
        &.active{
          display: block;
        }
      }
    }
  }
</style>
