---
title: 研究夏目漱石作品的用词风格及其变化——基于MeCab分词程序
tags: 研究计划书, 2017
grammar_cjkRuby: true
---

[toc]

# 研究主题
研究夏目漱石作品的用词风格及其变化——基于MeCab分词程序

# 研究契机
笔者从2014年起学习编程，并在今年寒假期间接触人工智能和自然语言处理相关内容。在考入北京外国语大学日语系之后，笔者一直在思考如何将计算机技术与本专业知识结合，而在上网检索之后，笔者发现了日文分词软件——MeCab。将日文原文导入MeCab后，即可将文章中的所有句子以单词为单位分开，并分析出其词性。夏目漱石作为日本著名作家，在日本文学史上具有较高的地位，而青空文库上保存有日本著名作家夏目漱石的上百部文学作品，数量庞大，因此在众多作家中，研究夏目漱石的作品相对更为合适。于是，笔者准备从词频分析入手，对夏目漱石的用词风格进行分析，进而分析其语言风格及变化。

# 先行研究概述
## MeCab分词软件及其性能
> MeCabは 京都大学情報学研究科−日本電信電話株式会社コミュニケーション科学基礎 研究所共同研究ユニットプロジェクトを通じて開発されたオープンソース形態素解析 エンジンです。 言語, 辞書,コーパスに依存しない汎用的な設計を基本方針としています 。

经过长期的研究、探索，日文分词技术已经相当成熟。其中MeCab使用较为广泛，且使用难度小、运行速度快，可以进行大规模的统计和研究。因此，本文将会使用MeCab工具，配合语料库进行研究。

## 青空文库

青空文库是一个可以下载著作权保护期已满的作品的网站，青空文库现有作品约15000部，其中约13500部著作权保护期已满。夏目漱石的作品中，有《我是猫》、《哥儿》、《心》等100部能直接从青空文库免费获取。因此，从青空文库下载夏目漱石的作品并处理是可行的。

## Python编程语言

本文将采用Python语言作为编程工具，Python语言的主要特点是轻量、第三方库丰富，适合快速完成统计工作并将研究结果用图标、动画等形式直观地显示出来。

# 研究方法

本文计划从青空文库下载夏目漱石的全部作品，并保留其中大多数作品，对每一部进行分词处理后，进行词频统计与分析，并与语料库中该词语出现的频率相比较，找出一些“特殊”的词汇，借此分析夏目漱石的用词特点。

# 准备与进展情况

笔者在个人电脑上，对夏目漱石的作品《我是猫》进行了初步处理，处理用时仅3.5秒，而《我是猫》属于夏目漱石作品中属于篇幅较长的。因此，笔者认为，对夏目漱石的所有作品进行上述研究在时间和空间上是可行的。

程序如下：
```python
import time
time0 = time.time()
import sys
sys.setrecursionlimit(100000)  # set the maximum depth as 1500
# 以上为必要的前期处理 以下为逻辑部分

import MeCab


def filter(text):
    # 将原文中“［］《》”之间的文字(青空文库格式txt文件中的)删除
    # 传入一个字符串，输出过滤后的字符串
    flag = True
    news = ''
    for char in text:
        if char in '［《':
            flag = False
        if flag:
            news += char
        if char in '］》':
            flag = True
    return news

def sort(words):
    # 为单词计数列表排序，使用归并排序算法，传出有小到大排序后的列表
    if len(words) <= 1:
        return words
    else:
        small  = []
        big    = []
        middle = words.pop()
        for word in words:
            if word[0] > middle[0]:
                big.append(word)
            else:
                small.append(word)
        return sort(small) + [middle] + sort(big)

with open('wagahaiwa_nekodearu.txt', encoding = 'shift-JIS') as textfile:
    text = textfile.read()
    text = filter(text)
# 读取作品「我輩は猫である」并处理

m = MeCab.Tagger("")                # MeCab分词器初始化
words = m.parse(text).split('\n')   # 分词处理

dictcounter = {}

for word in words:                  # 词语计数
    if word in dictcounter:
        dictcounter[word] += 1
    else:
        dictcounter[word] = 1

words = []

for word in dictcounter:            # 将字典中的计数信息转到列表中以方便排序
    count = dictcounter[word]
    words.append((count, word))

words = sort(words)                 # 对列表排序
for word in words[:-100:-1]:        # 输出计数最高的100个词
    print(word[0], word[1])
print(time.time() - time0)          # 显示程序运行用时

```
运行结果如下：
```
7486 。 記号,句点,*,*,*,*,。,。,。
7031 の 助詞,連体化,*,*,*,*,の,ノ,ノ
6817 て 助詞,接続助詞,*,*,*,*,て,テ,テ
6773 、 記号,読点,*,*,*,*,、,、,、
6424 は 助詞,係助詞,*,*,*,*,は,ハ,ワ
6071 を 助詞,格助詞,一般,*,*,*,を,ヲ,ヲ
5495 に 助詞,格助詞,一般,*,*,*,に,ニ,ニ
4200 が 助詞,格助詞,一般,*,*,*,が,ガ,ガ
3974 た 助動詞,*,*,*,特殊・タ,基本形,た,タ,タ
3547 と 助詞,格助詞,引用,*,*,*,と,ト,ト
            ···中略 共100行···
260 さん        名詞,接尾,人名,*,*,*,さん,サン,サン
257 方  名詞,非自立,一般,*,*,*,方,ホウ,ホー
249 猫  名詞,一般,*,*,*,*,猫,ネコ,ネコ
245 だけ        助詞,副助詞,*,*,*,*,だけ,ダケ,ダケ
241 云っ        動詞,自立,*,*,五段・ワ行促音便,連用タ接続,云う,ユッ,ユッ
232 思っ        動詞,自立,*,*,五段・ワ行促音便,連用タ接続,思う,オモッ,オモッ
3.1022138595581055
```
# 参考文献

[1] [MeCab: Yet Another Part-of-Speech and Morphological Analyzer][3]
（http://taku910.github.io/mecab/）
[2] 李航.统计学习方法[M].北京：清华大学出版社，2012.


  [3]: http://taku910.github.io/mecab/