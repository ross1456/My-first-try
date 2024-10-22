# 地址分割与地理位置提取

本项目通过自然语言处理（NLP）技术执行地址分割和地理坐标提取。它利用 OpenAI 模型和 transformers 模型，自动将地址划分为多个字段，并预测纬度/经度坐标。

## 项目结构

- **NER 提示词 1（地址分割）**：自动将地址划分为建筑名称、街道、城市、邮政编码和国家等字段。
- **NER 提示词 2（地理位置提取）**：识别并返回给定地址的地理坐标（纬度和经度）。

### 主要功能:
- **地址分割**：将地址分解为不同的组件。
- **地理位置提取**：从原始地址中获取纬度和经度。
- **基于 NLP 的处理**：使用 transformers 和 OpenAI API 进行地址处理。

## 安装

使用以下命令安装必要的依赖项：

```bash
pip install -r requirements.txt
```

## 使用说明

1. 运行上述命令安装依赖。
2. 准备好您的数据，提供包含地址信息的 CSV 文件。
3. 运行 notebook 生成 NER 提示词，并应用模型进行地址分割和地理坐标提取。

### 示例代码

```python
# 生成地址分割的 NER 提示词
org_addr = "1600 Amphitheatre Parkway, Mountain View, CA"
filled_prompt_1 = generate_ner_prompt(NER_PROMPT_1, org_addr)
print(filled_prompt_1)

# 生成地理位置提取的 NER 提示词
filled_prompt_2 = generate_ner_prompt(NER_PROMPT_2, org_addr)
print(filled_prompt_2)
```

## 函数定义

项目中的重要功能几乎都被封装为函数，具体如下：

- **`create_table(df)`**：创建数据库表结构，定义字段如 `building_name`。该函数将数据构造成数据库表的形式，便于后续处理和查询。
- **`generate_ner_prompt(prompt, org_addr)`**：使用给定的地址信息填充提示词，生成适合进一步任务处理的文本。
- **`apply_template(tokenizer, prompt)`**：将生成的提示词转换为适合模型处理的格式，可能会与 `tokenizer` 和 transformers 模型交互。

## 数据加载

代码使用 `pandas` 读取 CSV 文件，加载政府数据库和需要处理的数据集。这些数据集的地址信息将被解析和处理。

## 主函数执行

在 `if __name__ == '__main__':` 代码块中，执行主要流程：

- 加载包括政府数据库和需要处理的地址在内的数据集。
- 使用 `get_geoaddr` 函数，对地址进行分割并处理地理位置。

## 数据集
- **输入 1**：包含政府数据库的 CSV 文件。
- **输入 2**：包含需要处理的地址数据集的 CSV 文件。

### 数据列:
- **政府数据库 CSV**：包含官方的地址数据。
- **地址数据集 CSV**：包含需要处理的原始地址信息。

## 依赖要求

- Python 3.8+
- OpenAI API 密钥（如果使用 OpenAI 进行模型推理）
- 包含地址数据的 CSV 文件


## 许可协议

本项目采用 MIT 许可协议。
