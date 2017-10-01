#HSLIDE

### AI, NLP in chatbot
<!-- #### các vấn đề hiện đại trong công nghệ thông tin -->

<span style="color:gray">Nhóm 10</span>

---

### API.AI

  - Api.ai là một framework hỗ trợ xử lý ngôn ngữ tự nhiên nhằm hỗ trợ người lập trình xây dựng một công cụ liên quan đến giao tiếp tự động giữa người và máy tính.
  - Api.ai’s Speech Recognition
  - Natural Language Understanding and Conversation Management

---

### Natural Language Processing

<ol>
<li class="fragment" data-fragment-index="1"><span style="font-weight: bold">Lexical Category</span> – Nhóm từ vựng học</li>
<li class="fragment" data-fragment-index="2"><span style="font-weight: bold">Pattern</span> – cú pháp hay ngữ pháp hình thành trong một câu</li>
<li class="fragment" data-fragment-index="3"><span style="font-weight: bold">Intent</span> – xác định ý định, hay mục đích của câu được phân tích dựa trên ngữ cảnh giao tiếp.</li>
</ol>

---

### Lexical Category

- Nhóm từ vựng học
- Khái niệm này giúp định danh cho một tập các từ hoặc cụm từ cùng mang một ý nghĩa hay đề cập đến một nội dung cụ thể.
- Ví du: Food là một Lexical Category bao gồm các từ như bún bò, hủ tiếu, …

+++

### Example

![Example](assets/image01.jpg)

+++

### AWSTask

<span style="color:gray">An executable object that represents an AWS Gateway call.</span>

```Java
AWSTask aTask = AWS.Task(gateway)
                   .resource("/echo")
                   .get();

```

+++

### AWSResult

<span style="color:gray">An object that represents the result of an AWS Gateway call.</span>

```Java
AWSResult aResult = aTask.execute();
```

---

### SAMBA + Apache Spark Batch Processing

+++

#### Step 1. Build RDD[<span style="color:gray">AWSTask</span>]

```Scala
import io.onetapbeyond.lambda.spark.executor.Gateway._
import io.onetapbeyond.aws.gateway.executor._

val aTaskRDD = dataRDD.map(data => {
  AWS.Task(gateway)
     .resource("/score")
     .input(data.asInput())
     .post()
  })
```

+++

#### Step 2. Delegate RDD[<span style="color:gray">AWSTask</span>]

```Scala
// Perform RDD[AWSTask].delegate operation to execute
// AWS Gateway calls and generate resulting RDD[AWSResult].

val aResultRDD = aTaskRDD.delegate
```

+++

#### Step 3. Process RDD[<span style="color:gray">AWSResult</span>]

```Scala
// Process RDD[AWSResult] data per app requirements.

aTaskResultRDD.foreach { result => {
        println("TaskDelegation: compute score input=" +
          result.input + " result=" + result.success)
}}
```

+++?gist=494e0fecaf0d6a2aa2acadfb8eb9d6e8

---

#### SAMBA Deployment Architecture

![SAMBA Deployment](https://onetapbeyond.github.io/resource/img/samba/new-samba-deploy.jpg)

---

#### Some Related Links

- [GitHub: SAMBA Package](https://github.com/onetapbeyond/lambda-spark-executor)
- [GitHub: SAMBA Examples](https://github.com/onetapbeyond/lambda-spark-executor#samba-examples)
- [GitHub: aws-gateway-executor](https://github.com/onetapbeyond/aws-gateway-executor)
- [GitHub: Apache Spark](https://github.com/apache/spark)
- [Apache Spark Packages](https://spark-packages.org/package/onetapbeyond/lambda-spark-executor)
