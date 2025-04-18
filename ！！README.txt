第一步：txt_segmentation.py（文本三粒度切分）

##过滤表格标记暂时不用在意，是之前拿到的word里面包含各种表格做的过滤操作

返回结果是segmentation文件夹里的三个粒度数据（已创建好关系），可以直接灌库

第二步：table_segmentation.py（表格二粒度切分）

##目前只写了excel转换成csv的逻辑o

##表格只保存原始表格，中粒度切分内容

————————————数据切分工作完成——————————————————

第三步：knowledge_augment.py（数据增强）+ prompt.py

##增强文本粗粒度（段落）、文本中粒度（句子）、表格中粒度 数据

##结果保存在augement_data文件夹中

第四步：data_table_description

##表格表头字段增强+表格整体概括

##返回内容保存在table_storage中的table_descriptions文件夹中

注意！！表格的两种增强保存在不同的目录

————————————数据增强工作完成——————————————————

第五步：Graph_start

##数据灌库

存在三种关系类型：父子继承关系：CONTAINS  /  表格增强关系：HAS_DESCRIPTION  /  三元组内部关系：SEMANTIC

##基础知识图谱构建成功

第六步：export_neo4j.py

##从基础知识图谱中导出所有节点、节点属性，以及已经存在的关系

##导出至exported_data文件夹下

第七步：es_neo4j.py + es_engine.py

##将neo4j导出的内容灌入es向量库，进行编码以及内部匹配

##匹配方案：跳过节点自身，节点原始关系，取topk + 20，vector_match阈值设为0.8

第八步：mix_relation.py

##导入匹配关系，以及vector match的分数（作为匹配关系的属性）

————————————知识图谱构建完成——————————————————

##游走算法还需要沉淀一下 可以先不看（random_walk_strategies.py + walk_start.py）

data_clean.py都是之前处理不规则表格用的小工具

multi_head_paeser.py是表头整合小工具

PDFtable_extract.py是pdf表格提取小工具（项目暂时用不到了）

text_clean.py是文本清理小工具（暂时用不到了）














