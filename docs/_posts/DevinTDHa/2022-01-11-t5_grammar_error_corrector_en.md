---
layout: model
title: T5 for grammar error correction
author: John Snow Labs
name: t5_grammar_error_corrector
date: 2022-01-11
tags: [t5, en, open_source]
task: Text Generation
language: en
edition: Spark NLP 3.1.0
spark_version: 3.0
supported: true
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

This is a text-to-text model fine tuned to correct grammatical errors when the task is set to "gec:". It is based on Prithiviraj Damodaran's Gramformer model.

## Predicted Entities



{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/t5_grammar_error_corrector_en_3.1.0_3.0_1641914669661.zip){:.button.button-orange.button-orange-trans.arr.button-icon}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
import sparknlp
from sparknlp.base import *
from sparknlp.annotator import *

spark = sparknlp.start()

documentAssembler = DocumentAssembler() \
    .setInputCol("text") \
    .setOutputCol("documents")

t5 = T5Transformer.pretrained("t5_grammar_error_corrector") \
    .setTask("gec:") \
    .setInputCols(["documents"]) \
    .setMaxOutputLength(200) \
    .setOutputCol("corrections")

pipeline = Pipeline().setStages([documentAssembler, t5])
data = spark.createDataFrame([["He are moving here."]]).toDF("text")
result = pipeline.fit(data).transform(data)
result.select("corrections.result").show(truncate=False)
```
```scala
import spark.implicits._
import com.johnsnowlabs.nlp.base.DocumentAssembler
import com.johnsnowlabs.nlp.annotators.seq2seq.T5Transformer
import org.apache.spark.ml.Pipeline

val documentAssembler = new DocumentAssembler()
  .setInputCol("text")
  .setOutputCol("documents")

val t5 = T5Transformer.pretrained("t5_grammar_error_corrector")
  .setTask("gec:")
  .setMaxOutputLength(200)
  .setInputCols("documents")
  .setOutputCol("corrections")

val pipeline = new Pipeline().setStages(Array(documentAssembler, t5))

val data = Seq("He are moving here.").toDF("text")
val result = pipeline.fit(data).transform(data)

result.select("corrections.result").show(false)
```
</div>

## Results

```bash
+--------------------+
|result              |
+--------------------+
|[He is moving here.]|
+--------------------+
```

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|t5_grammar_error_corrector|
|Compatibility:|Spark NLP 3.1.0+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[documents]|
|Output Labels:|[corrections]|
|Language:|en|
|Size:|926.2 MB|