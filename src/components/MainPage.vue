<template>
    <div class="myDiv">
        <div id="viz"></div>
        <el-text size="large">Query:</el-text>
        <br/>
        <el-text tag="mark">
            注意：查询是刷新当前视图，替换为新视图，更新是在当前视图上更新查询节点有关的所有节点,将鼠标放到节点上获取节点信息
        </el-text>
        <el-input
                v-model=val
                placeholder="请输入要查询的节点名称，例如：沼泽大尾莺"
                class="input-with-select"
        >
            <template #suffix>
                <el-button-group>
                    <el-button type="primary" @click="submit(0)">查询</el-button>
                    <el-button type="primary" @click="submit(1)">更新</el-button>
                </el-button-group>
            </template>
        </el-input>
    </div>
</template>

<script setup>
import NeoVis from "neovis.js";
import {onMounted, ref} from "vue";


var viz = {}; //定义一个viz对象
const val = ref();

onMounted(() => {
    draw()
}) //渲染


const submit = r => {
    if (r === 0) {
        const cypher = `MATCH (startNode)-[r]-(relatedNode) WHERE startNode.value = \"${val.value}\" RETURN startNode, r, relatedNode`
        viz.renderWithCypher(cypher);
    } else {
        const cypher = `MATCH (startNode)-[r]-(relatedNode) WHERE startNode.value = \"${val.value}\" RETURN startNode, r, relatedNode`
        viz.updateWithCypher(cypher);
    }
}

const draw = () => {
    // //simple
    // const config = {
    //     containerId: "viz",
    //     neo4j: {
    //         serverUrl: "neo4j://cac9873b.databases.neo4j.io",
    //         serverUser: "neo4j",
    //         serverPassword: "QBRTRu3zS5A8m3gJfhDi4wEoS-NtlqLyunPVyAxYhkw",
    //         driverConfig: {
    //             encrypted: "ENCRYPTION_ON",
    //             trust: "TRUST_SYSTEM_CA_SIGNED_CERTIFICATES"
    //         },
    //     },
    //     labels: {
    //         Bird: {
    //             value: "value",
    //         },
    //         Iris: {
    //             value: "value",
    //         }
    //     },
    //     initial_cypher: "MATCH (n:`鸟`) RETURN n LIMIT 25;"
    // }

    const config = {
        container_id: "viz",
        server_url: "neo4j://cac9873b.databases.neo4j.io",
        server_user: "neo4j",
        server_password: "QBRTRu3zS5A8m3gJfhDi4wEoS-NtlqLyunPVyAxYhkw",
        encrypted: "ENCRYPTION_ON",
        trust: "TRUST_SYSTEM_CA_SIGNED_CERTIFICATES",
        labels: {
            "Bird": {
                "caption": "value",
            },
            "Foot": {
                "caption": "value",
            },
            "Mouse": {
                "caption": "value",
            },
            'Iris': {
                "caption": "value",
            },
            "Genus": {
                "caption": "value",
            },
            "Family": {
                "caption": "value",
            },
            "Order": {
                "caption": "value",
            },
        },
        arrows: true,
    }

    viz = new NeoVis(config);
    viz.render();
    viz.updateWithCypher("MATCH (n:Bird) RETURN n LIMIT 25;");
    console.log(viz)
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