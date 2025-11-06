<template>
  <div class="app-container">
    <!-- 主区域卡片 -->
    <div class="card">
      <!-- 字段选择区域 -->
      <div class="field-area">
        <h3>选择字段</h3>
        <div class="field-buttons">
          <button
            v-for="field in fields"
            :key="field.name"
            class="field-button"
            @click="addField(field)"
          >
            {{ field.label }}
          </button>
        </div>
      </div>

      <!-- 操作符选择区域 -->
      <div class="operator-area">
        <h3>选择操作符</h3>
        <div class="operator-buttons">
          <button
            v-for="op in operators"
            :key="op"
            class="operator-button"
            @click="addOperator(op)"
          >
            {{ op }}
          </button>
        </div>
      </div>
    </div>

    <!-- 表达式显示和控制区 -->
    <div class="expression-card">
      <textarea class="expression-input" v-model="expression" readonly></textarea>
      <div class="control-buttons">
        <button class="clear-button" @click="clearExpression">清空</button>
        <button class="output-button" @click="outputExpression">生成</button>
      </div>
    </div>

    <!-- 输出结果 -->
    <div class="output-panel">
      <h3>生成的逻辑表达式</h3>
      <pre>{{ expression }}</pre>
    </div>
  </div>
</template>

<script setup lang="ts">
// 字段类型定义
interface FormType {
  name: string;
  label: string;
  type: string;
  value: string;
}

// 字段列表类型
type Fields = FormType[];

// 操作符类型定义
type Operator = '&&' | '||' | '(' | ')';

// 字段数据
const fields: Fields = [
  { name: 'name', label: '姓名', type: 'string', value: '' },
  { name: 'age', label: '年龄', type: 'number', value: '' },
  { name: 'address', label: '地址', type: 'string', value: '' },
];

// 操作符数据
const operators: Operator[] = ['&&', '||', '(', ')'];

// 表达式状态
import { ref } from 'vue';
const expression = ref('');

// 添加字段
const addField = (field: FormType) => {
  expression.value += field.name;
};

// 添加操作符
const addOperator = (op: Operator) => {
  expression.value += ` ${op} `;
};

// 清空表达式
const clearExpression = () => {
  expression.value = '';
};

// 输出表达式
const outputExpression = () => {
  alert(`生成的逻辑表达式：${expression.value}`);
};
</script>

<style scoped>
/* 全局样式 */
.app-container {
  font-family: 'Arial', sans-serif;
  max-width: 900px;
  margin: 20px auto;
  padding: 20px;
  color: #333;
}

/* 卡片样式 */
.card {
  display: flex;
  justify-content: space-between;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
}

/* 字段区和操作符区 */
.field-area,
.operator-area {
  flex: 1;
  margin: 0 10px;
  text-align: center;
}

h3 {
  margin-bottom: 10px;
  font-size: 1.2em;
  color: #555;
}

/* 按钮样式 */
.field-button,
.operator-button {
  margin: 5px;
  padding: 10px 15px;
  background: linear-gradient(45deg, #4caf50, #81c784);
  border: none;
  color: white;
  font-weight: bold;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s;
}

.field-button:hover,
.operator-button:hover {
  background: linear-gradient(45deg, #388e3c, #66bb6a);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

/* 表达式显示框 */
.expression-card {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

textarea.expression-input {
  width: 100%;
  height: 80px;
  padding: 10px;
  font-size: 1em;
  border: 1px solid #ddd;
  border-radius: 5px;
  resize: none;
  margin-bottom: 15px;
}

/* 控制按钮样式 */
.control-buttons {
  display: flex;
  justify-content: space-between;
}

.clear-button,
.output-button {
  padding: 10px 20px;
  font-size: 1em;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s;
}

.clear-button {
  background: #e53935;
}

.clear-button:hover {
  background: #c62828;
}

.output-button {
  background: #1e88e5;
}

.output-button:hover {
  background: #1565c0;
}

/* 输出结果样式 */
.output-panel {
  margin-top: 20px;
  padding: 20px;
  background: #f4f4f4;
  border-radius: 10px;
  font-size: 1em;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
