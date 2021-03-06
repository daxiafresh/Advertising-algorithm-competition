# ctr 算法竞赛总结


## 1、阿里妈妈和腾讯广告算法大赛总结

详情参考 [2018IJCAI-阿里妈妈广告搜索转化预测大赛/腾讯广告算法大赛总结](https://zhuanlan.zhihu.com/p/38202468)

## 2、讯飞广告营销算法大赛

初赛，复赛均为第 24 名。

三套代码, 两个 lgb 模型，所用特征有稍微差异；另外一个使用 onehot 处理 category 特征，一个没有。第三个是 lgb叶子节点特征 + onehot 处理过后的特征，使用 LR 模型，在整理代码时我尝试使用全连接神经网络来代替逻辑回归，但是最终因为数据太稀疏，导致全连接参数众多，所以训练速度非常慢，所以我并没有训练完，所以不知道效果如何，读者如果需要尝试，可以将全连接替换成 LR 模型。

比赛结束后，我对代码进行了整理，往原始代码里添加了一些其他人的开源特征，实际效果没测试；另外 `lgb_model2.py` 文件基本使用的是林有夕的代码。

## 3、天池OGeek算法挑战赛

代码`oppo_instance_search_ctr.py` 里面有详细注释。复赛暂时50名，但是上传的代码线上只有 0.7058 的分数，可能需要调整一下正负例的分割阈值，总的来说在怎么调整分数也不会很高。

### 代码思路：

- 利用 prefix_prediction 字段对 prefix 进行拼写纠错改写
- 检查 prefix_prediction 中是否有大于 0.1 的概率的候选项，如果有，则计算该候选项和 title 之间的相似度，召回率，准确率，精确率
- 计算 prefix 是否完整出现在 title 中，并且定位其出现的位置（前，后，中）
- 计算 prefix、title 、tag、以及他们的两两组合转换率，构造组合特征并进行 onehot 处理
- 计算 prefix 和 title 的 1-2gram 相似度，点乘、余弦相似度等相似度，具体见代码
- 对 prefix 和 title 进行 SVD 矩阵分解，得到这些句子的语义向量，然后对 prefix 和 title语义向量进行交互，具体见代码
- 计算 prefix 针对于 title 的召回率，精确率，准确率，详情见代码
- 计算 prefix 长度，以及和 tag 的组合的转换率

## 4、2019腾讯广告算法大赛

赛题背景：

本次算法大赛的题目是源于腾讯广告业务中一个面向广告主服务的真实业务产品 ——广告曝光预估。广告曝光预估的目的是在广告主创建新广告和修改广告设置时，为广告主提供未来的广告曝光效果参考。通过这个预估参考，广告主能避免盲目的优化尝试，有效缩短广告的优化周期，降低试错成本， 使广告效果尽快达到广告主的预期范围。
简单来说，就是广告主想要投放广告，我们需要通过预测告诉他，在不同的出价情况下，他的广告会有多少的曝光。这时候广告主可以在出价和曝光量之间权衡选择，在可接受的价钱下得到合适的曝光量。

**线上最终成绩：RANK 15，决赛 RANK 13 (应该是有两个队伍没提交代码)**

[代码](https://github.com/wangle1218/Advertising-algorithm-competition/tree/master/2019tengxun)

竞赛总结 [2019腾讯广告算法大赛 RANK 15 解决方案分享](https://mp.weixin.qq.com/s/9lhc9eZakOE1P8wuo4Hrnw)




## 如果对你有帮助就点个小星星啊，后期有空将整理一下阿里妈妈和腾讯两个比赛的top开源代码，并做简单解释和统一规范处理成 pipeline（预留坑）