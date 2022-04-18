---
layout: model
title: Hindi RoBERTa Embeddings (from surajp)
author: John Snow Labs
name: roberta_embeddings_RoBERTa_hindi_guj_san
date: 2022-04-14
tags: [hi, open_source]
task: Embeddings
language: hi
edition: Spark NLP 3.4.2
spark_version: 3.0
supported: true
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained RoBERTa Embeddings model, uploaded to Hugging Face, adapted and imported into Spark NLP. `RoBERTa-hindi-guj-san` is a Hindi model orginally trained by `surajp`.

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/roberta_embeddings_RoBERTa_hindi_guj_san_hi_3.4.2_3.0_1649947496602.zip){:.button.button-orange.button-orange-trans.arr.button-icon}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = DocumentAssembler() \
    .setInputCol("text") \
    .setOutputCol("document")

tokenizer = Tokenizer() \
    .setInputCols("document") \
    .setOutputCol("token")
  
embeddings = RoBertaEmbeddings.pretrained("roberta_embeddings_RoBERTa_hindi_guj_san","hi") \
    .setInputCols(["document", "token"]) \
    .setOutputCol("embeddings")
    
pipeline = Pipeline(stages=[documentAssembler, tokenizer, embeddings])

data = spark.createDataFrame([["मुझे स्पार्क एनएलपी पसंद है"]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val documentAssembler = new DocumentAssembler() 
      .setInputCol("text") 
      .setOutputCol("document")
 
val tokenizer = new Tokenizer() 
    .setInputCols(Array("document"))
    .setOutputCol("token")

val embeddings = RoBertaEmbeddings.pretrained("roberta_embeddings_RoBERTa_hindi_guj_san","hi") 
    .setInputCols(Array("document", "token")) 
    .setOutputCol("embeddings")

val pipeline = new Pipeline().setStages(Array(documentAssembler, tokenizer, embeddings))

val data = Seq("मुझे स्पार्क एनएलपी पसंद है").toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|roberta_embeddings_RoBERTa_hindi_guj_san|
|Compatibility:|Spark NLP 3.4.2+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[sentence, token]|
|Output Labels:|[bert]|
|Language:|hi|
|Size:|252.1 MB|
|Case sensitive:|true|

## References

- https://huggingface.co/surajp/RoBERTa-hindi-guj-san
- https://github.com/goru001/inltk
- https://www.kaggle.com/disisbig/hindi-wikipedia-articles-172k
- https://www.kaggle.com/disisbig/gujarati-wikipedia-articles
- https://www.kaggle.com/disisbig/sanskrit-wikipedia-articles
- https://twitter.com/parmarsuraj99
- https://www.linkedin.com/in/parmarsuraj99/