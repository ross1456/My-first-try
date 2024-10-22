# 基于RAG和AI大模型标准化客户地址数据

本项目通过检索增强生成(RAG)以及自然语言处理（NLP）技术执行地址分割和地理坐标提取。它利用 Llama3, BGE reranker等多个模型，自动将地址划分为多个字段，并生成GeoAddress编号。


## 项目结构:
- **调用模型**通过API调用大语言模型（Hagging Face Llama3）
- **地址分割**：标准化地将地址切割为不同部分。
- **向量化**：利用BGE-base-en-v1.5嵌入式模型，将字符串转换成向量表示。
- **Query**：先从数据库中搜索，如未能匹配则从向量数据库中获取相似地址并重新排序(BGE-Reranker)，反之直接返回结果。
- **地理位置提取**：根据query和相似地址，生成提示词向语言模型查询并输出标准化输出。

## 安装

使用以下命令安装必要的依赖项：

```bash
pip install -r requirements.txt
```

## 使用说明

1. 运行上述命令安装依赖。
2. 准备好您的数据，提供包含地址信息的 CSV 文件。
3. 运行 notebook 生成 NER 提示词，并应用模型进行地址分割和地理坐标提取。


## 数据加载

代码使用 `pandas` 读取 CSV 文件，加载政府数据库和需要处理的数据集。这些数据集的地址信息将被解析和处理。

## 主函数执行

在 `if __name__ == '__main__':` 代码块中，执行主要流程：

- 加载包括政府数据库和需要处理的地址在内的数据集。
- 使用 `get_geoaddr` 函数，对地址进行分割并处理地理位置。

## 数据集
- **data/database.csv**：包含政府数据库的 CSV 文件。
- **data/input.csv**：包含需要处理的地址数据集的 CSV 文件。

## 依赖要求

- Python 3.8+
- OpenAI API 密钥（如果使用 OpenAI 进行模型推理）
- 包含地址数据的 CSV 文件
