<template>
    <div class="myDiv">
        <div id="viz"></div>
        Query:
        <el-input
                v-model=val
                placeholder="请输入要查询的节点名称，例如：沼泽大尾莺"
                class="input-with-select"
        >
            <template #suffix>
                <el-button-group>
                    <el-button type="primary" @click="submit">Submit</el-button>
                    <el-button type="primary" @click="stabilize">Stabilize</el-button>
                </el-button-group>
            </template>
        </el-input>
    </div>
</template>

<script setup>
import NeoVis from "neovis.js";
import {onMounted, ref} from "vue";


let viz = {}; //定义一个viz对象
const val = ref();

onMounted(() => {
    draw()
}) //渲染


const submit = () => {
    if (val.value != null) {
        const cypher = `MATCH (startNode)-[r]-(relatedNode) WHERE startNode.value = \"${val.value}\" RETURN startNode, r, relatedNode`
        viz.renderWithCypher(cypher);
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