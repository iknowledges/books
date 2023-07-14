# Chapter 16. Natural Language Processing with RNNs and Attention

## Generating Shakespearean Text Using a Character RNN

### Creating the Training Dataset

First, using Keras’s handy `tf.keras.utils.get_file()` function, let’s download all of
Shakespeare’s works. The data is loaded from Andrej Karpathy’s [char-rnn project](https://github.com/karpathy/char-rnn):

```python
import tensorflow as tf
shakespeare_url = "https://homl.info/shakespeare"
# shortcut URL
filepath = tf.keras.utils.get_file("shakespeare.txt", shakespeare_url)
with open(filepath) as f:
    shakespeare_text = f.read()
```

Let’s print the first few lines:

```python
print(shakespeare_text[:80])
```

Next, we’ll use a `tf.keras.layers.TextVectorization` layer to encode this text. We set split="character" to get character-level encoding rather than the default word-level encoding, and we use standardize="lower" to convert the text to lowercase:（使用`tf.keras.layers.TextVectorization`编码文本。设置split="character"进行字符级别的编码，而不是默认的词级别。设置standardize="lower"将字母全部转成小写。）

```python
text_vec_layer = tf.keras.layers.TextVectorization(split="character", standardize="lower")
text_vec_layer.adapt([shakespeare_text])
encoded = text_vec_layer([shakespeare_text])[0]
```

Each character is now mapped to an integer, starting at 2. The TextVectorization
layer reserved the value 0 for padding tokens, and it reserved 1 for unknown char‐
acters.（每个字符都映射到一个整数，从2开始。TextVectorization层保留了0作为填充标记，1作为未知标记。）

We won’t need either of these tokens for now, so let’s subtract 2 from the
character IDs and compute the number of distinct characters and the total number of
characters:

```python
encoded -= 2 # drop tokens 0 (pad) and 1 (unknown), which we will not use
n_tokens = text_vec_layer.vocabulary_size() - 2 # number of distinct chars = 39
dataset_size = len(encoded) # total number of chars = 1,115,394
```
