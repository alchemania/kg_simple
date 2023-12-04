<template>
    <div class="myDiv">
        <div id="viz"></div>
        <el-text size="large">Query:</el-text>
        <br/>
        <el-text tag="mark">
            Note: The "query" is to refresh the current view and replace it with a new view, the "update" is to update the query node on the current view with respect to all nodes, put the mouse on the node to get the node information.        
        </el-text>
        <el-input
                v-model=val
                placeholder="Please enter the name of the node to be queried, e.g., Swamp Great-tailed Warbler"
                class="input-with-select"
        >
            <template #suffix>
                <el-button-group>
                    <el-button type="primary" @click="submit(0)">Query</el-button>
                    <el-button type="primary" @click="submit(1)">Update</el-button>
                </el-button-group>
            </template>
        </el-input>
    </div>
</template>

<script setup>
import NeoVis from "neovis.js";
import {onMounted, ref} from "vue";
import {ElMessage} from "element-plus";


var viz = {}; //define
const val = ref();

onMounted(() => {
    draw()
}) //Render


const submit = r => {
    if (r === 0) {
        const cypher = `MATCH (startNode)-[r]-(relatedNode) WHERE startNode.value = \"${val.value}\" RETURN startNode, r, relatedNode`
        viz.renderWithCypher(cypher)
        ElMessage({
            type: "success",
            message: "Render successful"
        })
    } else {
        const cypher = `MATCH (startNode)-[r]-(relatedNode) WHERE startNode.value = \"${val.value}\" RETURN startNode, r, relatedNode`
        viz.updateWithCypher(cypher)
        ElMessage({
            type: "success",
            message: "Updated"
        })
    }
}

const draw = async () => {
    const config = {
        container_id: "viz",
        server_url: "Your Own Neo4j link",
        server_user: "neo4j",
        server_password: "Your Own password",
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
    try {
        await viz.updateWithCypher("MATCH (n) RETURN n LIMIT 25;")
        ElMessage({
            type: "success",
            message: "Initialized",
            duration: 2000
        })
    } catch (e) {
        ElMessage({
            type: "error",
            message: "Initialize Fail",
            duration: 2000
        })
    }

    console.log(viz)
}
</script>

<style lang="less" scoped>
.myDiv {
  width: 100%;
  height: 100%;
}

#viz {
  width: 100%;
  height: 80vh;
  border: 1px solid #f1f3f4;
  //font: 22pt arial;
}

input {
  border: 1px solid #ccc;
}
</style>
