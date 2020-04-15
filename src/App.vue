<template>
  <div id="app">
    <div id="_titleinfo" class="title-info" >
      <button id="_poptest" @click="PopupTest">按钮</button>
    </div>
    <div class="main-content">
      <div class="routediv">
        <router-view id="_routeView" />
      </div>
      <div ref="mapusediv" class="mapdiv">
        <object
          id="TerraExplorer3DWindow"
          ref="TE3DWindowEx"
          classid="CLSID:3a4f9192-65a8-11d5-85c1-0001023952c1"
          width="100%"
        ></object>

        <div class="emptydiv">
          <object
            id="SGWorld"
            classid="CLSID:3A4F919D-65A8-11D5-85C1-0001023952C1"
            style="visibility:hidden;"
            height="0"
            width="0"
          ></object>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var selfscope = this;
export default {
  name: "App",
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  },
  created() {
    selfscope = this;
  },
  mounted() {
    selfscope.initTE();
    SGWorld.Project.Open("fly文件的地址", false, "", "");

    window.onresize = function() {
      selfscope.initTE();
    };
  },
  methods: {
    initTE() {
      const _teWin = selfscope.$refs.TE3DWindowEx;
      const _parentdiv = document.getElementById("_routeView");
      _teWin.height = window.innerHeight - 50 + "px";
      _teWin.width = document.body.clientWidth - 300 + "px";
    },
    PopupTest() {
        alert(document.getElementById('_titleinfo').outerHTML);

      let _popInfo = SGWorld.Creator.CreatePopupMessage(
        "测试气泡",
        "",
        0,
        0,
        400,
        300,
        -1
      );
      _popInfo.InnerHTML ="<html><div>ssss</div> </html>";
      SGWorld.Window.ShowPopup(_popInfo);
    }
  }
};
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
}
.main-content {
  display: flex;
  flex-direction: row;
  margin: 0;
  padding: 0;
}

.title-info {
  height: 50px;
  display: flex;
  background-color: yellow;
}

.routediv {
  width: 300px;
  margin: 0px;
  padding: 0px;
}
.mapdiv {
  display: flex;
  background-color: red;
  margin: 0;
  padding: 0;
}
.emptydiv {
  width: 0;
  height: 0;
}
</style>
