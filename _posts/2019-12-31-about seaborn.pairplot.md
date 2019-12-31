---
layout: post
title: seaborn.pairplot的一些问题
published: true
---

### 以下内容来源于Kaggle上关于Tiantic排名第一的NoteBook

排名第一的笔记本使用了模型融合的方法，即Stacking

我在运行到seaborn.pairplot语句时

```
g = sns.pairplot(train[[u'Survived',
u'Pclass', u'Sex', u'Age',
u'Parch', u'Fare',
u'Embarked', u'FamilySize',
u'Title']],
hue='Survived',
palette = 'seismic',size=1.2,
diag_kind = 'kde',
diag_kws=dict(shade=True),
plot_kws=dict(s=10) )
g.set(xticklabels=[])
```

出现如下错误
![seaborn.pairplot](/images/seaborn.pairplot.png)

问题原因是因为"hue='Survived'"也是数值型，需要引入参与网格计算的变量“var=”,代码修改为

```
g = sns.pairplot(train[[u'Survived', u'Pclass', u'Sex', u'Age', u'Parch', u'Fare', u'Embarked',
       u'FamilySize', u'Title']],
        vars=train[[u'Pclass', u'Sex', u'Age', u'Parch', u'Fare', u'Embarked',
       u'FamilySize', u'Title']],
                 hue='Survived', palette = 'seismic',size=1.2,diag_kind = 'kde',diag_kws=dict(shade=True),plot_kws=dict(s=10) )
g.set(xticklabels=[])
```

问题解决
