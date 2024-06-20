<script setup>
  import { ref } from 'vue';
  
  const fileTree = ref([
    {
      name: 'OneDrive - Personal', type: 'folder', expanded: true, children: [
        {
          name: 'Documents', type: 'folder', expanded: false, children: [
            { name: 'Amvsoft', type: 'folder', expanded: false, children: [] },
            { name: 'Captura', type: 'folder', expanded: false, children: [] },
            { name: 'ClickCharts', type: 'folder', expanded: false, children: [] },
            { name: 'Custom Office Templates', type: 'folder', expanded: false, children: [] },
            { name: 'OneNote Notebooks', type: 'folder', expanded: false, children: [] },
            { name: 'Sound Recordings', type: 'folder', expanded: false, children: [] }
          ]
        },
        { name: 'Zoom', type: 'folder', expanded: false, children: [] },
        { name: 'Pictures', type: 'folder', expanded: false, children: [] },
        { name: 'TWC', type: 'folder', expanded: false, children: [] }
      ]
    }
  ]);
  
  const newNodeName = ref('');
  
  const toggleNode = (node) => {
    node.expanded = !node.expanded;
  };
  
  const addNode = () => {
    fileTree.value.push({ name: newNodeName.value, type: 'folder', expanded: false, children: [] });
    newNodeName.value = '';
  };
  </script>


<template>
    <div class="p-4">
      <ul>
        <li v-for="node in fileTree" :key="node.name">
          <div @click="toggleNode(node)" class="cursor-pointer flex items-center">
            <span>{{ node.expanded ? '📂' : '📁' }}</span>
            <span class="ml-2">{{ node.name }}</span>
          </div>
          <ul v-if="node.expanded" class="ml-4">
            <li v-for="child in node.children" :key="child.name">
              <div @click="toggleNode(child)" class="cursor-pointer flex items-center">
                <span>{{ child.expanded ? '📂' : '📁' }}</span>
                <span class="ml-2">{{ child.name }}</span>
              </div>
              <ul v-if="child.expanded" class="ml-4">
                <li v-for="grandchild in child.children" :key="grandchild.name">
                  <div class="cursor-pointer flex items-center">
                    <span>📄</span>
                    <span class="ml-2">{{ grandchild.name }}</span>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
      <div class="mt-4">
        <input v-model="newNodeName" placeholder="New Folder/File Name" class="border p-2 mr-2"/>
        <button @click="addNode" class="bg-blue-500 text-white px-4 py-2 rounded">Add</button>
      </div>
    </div>
  </template>