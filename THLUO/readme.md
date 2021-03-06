本代码运行在windows10, 48G内存, 1070ti显卡上, 由于运行的py文件比较多, 所以需要比较长的时间才能跑完

文件夹说明:
> cache文件夹是存放输出模型的文件夹
> embedding是存放w2c词嵌入的文件夹
> input是存放本次比赛数据的文件夹
> result是THLUO选手最终的结果

下面是每个py文件的功能介绍:
* 1.w2c_model_start.py	根据device打开app的时间对app进行排序，形成app_list, 将app开作词，device_id看成文档，对app进行embedding
* 2.w2c_model_close.py	根据device关闭app的时间对app进行排序，形成app_list, 将app开作词，device_id看成文档，对app进行embedding
* 3.w2c_model_all.py	根据device打开关闭app的时间合在对app进行排序，形成app_list, 将app开作词，device_id看成文档，对app进行embedding
* 4.device_quchong_start_app_w2c.py	根据device打开app的时间对app进行排序，形成app_list, 对app_list进行去重操作, 将app开作词，device_id看成文档，对app进行embedding
* 5.device_age_prob_oof.py	单独对用户年龄进行预测
* 6.device_sex_prob_oof.py	单独对用户性别进行预测
* 7.start_close_age_prob_oof.py	对app所属的年龄概率进行预测
* 8.start_close_sex_prob_oof.py	对app所属的性别概率进行预测
* 9.sex_age_bin_prob_oof.py	用2分类的手法来预测用户属于性别-年龄的概率
* 10.age_bin_prob_oof.py	用2分类的手法来预测用户属于年龄的概率
* 11.hcc_device_brand_age_sex.py	 手机品牌和手机类型属于High Cardinality Categorical,  参考论文A Preprocessing Scheme for High-Cardinality Categorical Attributes in Classification and Prediction Problems，对手机品牌和手机类型属于性别年龄的概率进行预测
* 12.device_age_regression_prob_oof.py	用回归的手法对用户属于年龄的概率进行预测
* 13.device_start_GRU_pred.py		根据device打开app的时间对app进行排序，形成app_list，将app开作词，device_id看成文档，跑了一个GRU文本模型对用户属于性别年龄的概率进行预测
* 14.device_start_GRU_pred_age.py		根据device打开app的时间对app进行排序，形成app_list，将app开作词，device_id看成文档，跑了一个GRU文本模型对用户属于年龄的概率进行预测
* 15.device_all_GRU_pred.py	根据device打开关闭app的时间合在对app进行排序，形成app_list, 将app开作词，device_id看成文档，跑了一个GRU文本模型对用户属于性别年龄的概率进行预测
* 16.device_start_capsule_pred.py		用capsule模型对用户属于性别年龄的概率进行预测
* 17.device_start_textcnn_pred.py		用textcnn模型对用户属于性别年龄的概率进行预测
* 18.device_start_text_dpcnn_pred.py	用dpcnn模型对用户属于性别年龄的概率进行预测
* 19.device_start_lstm_pred.py	用lstm模型对用户属于性别年龄的概率进行预测
* 20.lgb_sex_age_prob_oof.py		一个基础的模型，对用户属于性别年龄的概率进行预测
* 21.tfidf_lr_sex_age_prob_oof.py	对app进行tf-idf操作，用户LR训练一个模型来预测用户的性别年龄概率
* 22.base_feat.py		生成基础人工特征+上面产出的概率模型特征
* 23.ATT_v6.py	用attention模型对22.base_feat.py产出的特征进行训练，来计算用户属于性别年龄的概率
* 24.thluo_22_lgb.py	用lgb训练一个22多分类模型，输出test概率文件
* 25.thluo_22_xgb.py	用xgb训练一个22多分类模型，输出test概率文件
* 26.thluo_nb_lgb.py	用lgb训练一个条件分类模型，输出test概率文件，条件概率模型指的是先预测p(sex) 再预测p(age|sex),最终p(sex, age) = p(sex) * p(age|sex)
* 27.thluo_nb_xgb.py	用xgb训练一个条件分类模型，输出test概率文件，条件概率模型指的是先预测p(sex) 再预测p(age|sex),最终p(sex, age) = p(sex) * p(age|sex)
* 28.final.py	 	对上面四个模型产出的结果，进行线性加权融合，形成THLUO选手个人的最终结果
* TextModel.py包含本次比赛用到的文本模型
* util.py里面包含一些共用的函数




> note:因为本次比赛提交代码的时间比较仓促，之前一直都是用notebook来做比赛，所以如有问题，请联系团队
