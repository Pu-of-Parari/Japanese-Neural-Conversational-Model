# Japanese-Neural-Conversational-Model
- This the original implementation of [TesnorFlowTutorial](https://www.tensorflow.org/tutorials/)
- For TensorFlow v0.12 compatible version

- Wakati processing etc. are additionally implemented to correspond to Japanese ·

## 0.Set UP
This scripts is implemented by Python2 and TensorFlow v0.12.

`pip install -r requirements.txt`

In addition this, you should install MeCab.(I used ipadic-8)

## 1.Data Preparation
### 1.1 Getting Data
Get [the Nagoya University Conversation Corpus](https://mmsrv.ninjal.ac.jp/nucc/) using [this tool](https://github.com/knok/make-meidai-dialogue).
(The license follows the original.)

`mv sequence.txt ./predata/`

`$python data_prepro.py`

By runnning this code, you can obtain `input.txt` and `output.txt`.

### 1.2 Dividing Data
Divide each of the data for training and test set.

`split -l 30000 input.txt`

`split -l 30000 output.txt`

And rename the data to `{train,test}_data_{in,out}`.

Place the data as follows.(About `ids` and `vocab`, please prepare an empty file. )

```
chatbot
├── data
│   ├── test_data_ids_{in, out}.txt
│   ├── test_data_{in, out}.txt
│   ├── train_data_ids_{in,out}.txt
│   ├── train_data_{in, out}.txt
│   └── vocab_{in, out}.txt
│
├── predata
│   ├── data_prepro.py
│   └── sequence.txt
│
├── data_utils.py
├── seq2seq_model.py
└── translate.py
```
## 2.Traning
training model and create dictionary run:

`python transrate.py`

Since the loop range is not set, the model continues to learn.
If perplexity falls to some extent, please discontinue learning.
Because of without GPU, it takes a long time...

Even if you stop learning, learning will be resumed on the way by hitting the same command.

```:training
global step 82700 learning rate 0.0844 step-time 0.19 perplexity 2.46
  eval: bucket 0 perplexity 122.06
  eval: bucket 1 perplexity 242.77
  eval: bucket 2 perplexity 108.74
  eval: bucket 3 perplexity 126.07
global step 82800 learning rate 0.0836 step-time 0.17 perplexity 2.07
  eval: bucket 0 perplexity 21.42
  eval: bucket 1 perplexity 501.38
  eval: bucket 2 perplexity 145.67
  eval: bucket 3 perplexity 210.59
global step 82900 learning rate 0.0836 step-time 0.19 perplexity 2.49
  eval: bucket 0 perplexity 67.73
  eval: bucket 1 perplexity 66.10
  eval: bucket 2 perplexity 183.61
  eval: bucket 3 perplexity 26.17
global step 83000 learning rate 0.0827 step-time 0.18 perplexity 2.46
  eval: bucket 0 perplexity 100.90
  eval: bucket 1 perplexity 22.86
  eval: bucket 2 perplexity 57.99
  eval: bucket 3 perplexity 108.47
```


## 3.Decode mode
to decode run:

`python translate.py --decode`

You can chat with this system! Enjoy:)

```:example
> 名前は？
カーミちゃん。

> 何歳なの？
知らない。

> 元気にしてた？
してないね。

> 怒ってる？
ううん。

> カルシウム足りてないんじゃない？？
うん、たぶんね。

> 好きな食べ物って何かある？
おいしい、テレビで。
```

# LICENCE
The license of the used data set follows the original.

使用したデータセットのライセンスはオリジナルに従います。
