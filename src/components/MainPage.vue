<template>
    <div class="myDiv">
        <div id="viz"></div>
        Cypher query:
        <el-input
                v-model=obj
                :rows="2"
                type="textarea"
                placeholder="请输入你要查找的对象"
        />
        <br>
        <el-button-group>
            <el-button type="primary" @click="submit">Submit</el-button>
            <el-button type="primary" @click="stabilize">Stabilize</el-button>
        </el-button-group>
    </div>
</template>

<script setup>
import NeoVis from "neovis.js";
import {onMounted, ref} from "vue";


var viz = {} //定义一个viz对象
const obj = ref("MATCH (n:`鸟`) RETURN n LIMIT 25;");

onMounted(() => {
    draw()
}) //渲染


const submit = () => {
    if (obj.value.length > 3) {
        viz.renderWithCypher(obj.value);
        console.log(viz.nodes._data)
    } else {
        console.log("reload");
        viz.reload();
    }
}
const stabilize = () => {
    viz.stabilize();
}
const draw = () => {
    //simple
    const config = {
        containerId: "viz",
        neo4j: {
            serverUrl: "neo4j://cac9873b.databases.neo4j.io",
            serverUser: "neo4j",
            serverPassword: "QBRTRu3zS5A8m3gJfhDi4wEoS-NtlqLyunPVyAxYhkw",
            driverConfig: {
                encrypted: "ENCRYPTION_ON",
                trust: "TRUST_SYSTEM_CA_SIGNED_CERTIFICATES"
            }
        },
        // initial_cypher: "MATCH (n:`鸟`) RETURN n LIMIT 25;"
    }

    viz = new NeoVis(config);
    viz.render();
}

</script>

<style lang="less" scoped>
.myDiv {
  width: 1000px;
  height: 900px;
}

textarea {
  border: 1px solid lightgray;
  margin: 5px;
  border-radius: 5px;
}

#viz {
  width: 100%;
  height: 80%;
  border: 1px solid #f1f3f4;
  font: 22pt arial;
}

input {
  border: 1px solid #ccc;
}
</style>