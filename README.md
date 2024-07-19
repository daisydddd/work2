# 工作流程：
- 需求确认：用户建立对话，理解用户的需求。在这一阶段，会提出一系列问题，以便更准确地了解用户的需求。
- 任务规划：根据最终确认的需求内容为用户制定任务规划。这个规划包括一系列步骤，按照这些步骤来为用户提供服务。
- 任务执行：规划好的任务分配给不同的智能体，如数据查找智能体、SQL生成智能体、代码生成智能体、可视化分析智能体等。每个智能体负责其专业领域的任务执行，协同工作以确保任务的高效完成。
- 应用生成：根据用户需求任务将结果数据转化为数据API服务，这些成果能够以可视化的形式展示关键数据指标，提供API接口供其他系统或服务调用，以及根据用户需求生成具体的应用程序。

# 已实现的功能：
SQL生成、数据接入、知识库

# Start
## 环境要求
Python>=3.10
## 安装 airda
pip安装
pip install airda -i https://pypi.python.org/simple/
## 依赖安装
使用airda需要用到mongodb,可采用docker安装mongodb
#拉取mongo镜像
docker pull mongo
docker run -itd --name mongo -v /{path_of_mongo_data}:/data/db -p 27017:27017 mongo
## 自定义配置
环境变量

下载.env.template自定义embedding模型,mongo配置,以及openai配置

airda env load -p {your_path}/.env_template

日志文件（非必须）

下载log_config.yml.template,自定义日志配置

airda log load -p {your_path}/log_config.yml.template

Embedding Model

airda默认使用stella-large-zh-v2模型, 模型默认下载到~/.cache/huggingface/hub/路径,目录下没有需要手动下载

## 相关配置命令

添加你的数据源（目前只支持mysql，需改进！！！）

airda datasource add -n {datasource_name} -h {host} -p {port} -k MYSQL -d {database} -u {username} -w {password}

训练数据源的schema

airda datasource sync -n {datasource_name}

查询当前可用的数据源

airda datasource ls

## 开始问答

airda run cli -n {datasource_name}
#输入你的问题:
