### Jean-Philippe Bempel – Production profiling with JDK Flight Recorder & JDK Mission Control
Links: 
* https://github.com/thegreystone/java-svc/tree/master/jfr
* https://github.com/thegreystone/jmc-jshell/
* https://github.com/thegreystone/jmc-tutorial/
* https://github.com/brendangregg/FlameGraph/

*Rate*: 🌟 :star2:

### Otavio Santana – Framewars: the battle between NoSQL and Java in the cloud arena
*Rate*: 😪 :sleepy:
*Feedback:* an intro to different nosql and graph DB tools and frameworks. 

### Martin Toshev – Elasticsearch integrations
*Rate*: :star2:
*Feedback:* a good description of elasticsearch integration with a lot of codes inc. own plug-in 

### Иван Пономарёв – LJV: Чему нас может научить визуализация структур данных в Java
*Links*: https://github.com/atp-mipt/ljv
*Rate*: 🌟 :star2: 🔥 :fire: 💗 :heartpulse: 💪 :muscle: 🔁 :repeat:
*Feedback:* внешне простая идея, но насколько шикарно и легко работает в деле с визуализацией

### Юрий Бадальянц – Production-ready functional programming
*Rate*: 🌟 :star2: 🔥 :fire: 💪 :muscle:
*Feedback:* пример имплементации пула с полной мощью функционального программирования на Scala

### Алексей Игнатенко – Почему Java Enterprise бенчмарки врут, и что с этим делать
*Links*: some benchmarks for JVM 11 
  * https://github.com/chrisgleissner/benchmarks
   * fork with fixes https://github.com/KryukovaLidiya/benchmarks
*Rate*: 🌟 :star2: 🔥 :fire:
*Feedback:* для чего тестировать enterprise приложения и как, enterprise benchmarks и новый фреймворк TUSLA

### Алексей Шипелев - "Java-объекты наизнанку"
*Rate*: 🌟 :star2: 🔥 :fire:
Ссылочки про "Java-объекты наизнанку":
- слайды: https://shipilev.net/talks/snowone-Feb2021-javaobjec...
- пост: https://shipilev.net/jvm/objects-inside-out/

### Барух Садогурский - Как правильно продать себя ради фана и профита
*Rate*: 🌟 :star2: 🔥 :fire: 💪 :muscle: 🔁 :repeat:
*Links*:
* тест на персональность https://www.16personalities.com/ru/test-lichnosti
* подкаст https://newpodcast2.live/
* Книги:*
* Эрин Мейер "Карта культурных различий. Как люди думают, руководят и добиваются целей в международной среде" 
* Kim Scott "Radical Candor: Fully Revised & Updated Edition: Be a Kick-Ass Boss Without Losing Your Humanity" 

### Work shop 'Учимся готовить Spark'
*Links*:
* Quick prototyping with zeppelin - see :https://zeppelin.apache.org/docs/0.8.0/quickstart/install.html
* real Spark project https://github.com/asm0dey/gradle-spark-quickstart
*Rate*: 🌟 :star2: 🔥 :fire: 💗 :heartpulse: 💪 :muscle: 🔁 :repeat:
*Requirements:*
* Intellij Idea Ultimate
* Idea plug-ins: 'Big Data Tools', 'Scala'
* Activate a checkbox "Enable ZTools integration" in "Zeppelin Connection" settings 
*Feedback:* быстрая и интуитивно понятное знакомство с Spark
* Examples:
```
import org.apache.spark.sql.types.IntegerType

val df = spark.read
.option("header", true)
.option("inferSchema", true)
.csv("/home/dma/projects/hadoop-workshop/ml-latest/movies.csv")
.cache()

%

df
.filter($"title" rlike (""""?.*\(\d{4}\)\s*"?"""))
.withColumn("year", regexp_extract($"title", """\((\d{4})\)\s*"?""", 1).cast(IntegerType))
.withColumn("title", regexp_replace($"title", """\(\d{4}\)\s*"?""", ""))
.groupBy($"year")
.agg(count($"title"), $"year")
.createOrReplaceTempView("countOfMovies")


%spark.sql

SELECT `count(title)` as cnt, year
FROM countofmovies
WHERE year BETWEEN 1910 and 2016
ORDER BY year
%spark
import org.apache.spark.sql.types.{IntegerType, StringType}

case class Movie(movieId: Long, title: String, genres: String)

case class MovieWithYear(movieId: Long, title: String, genres: String, year: Integer)

case class MovieWithGenresAndYear(movieId: Long, title: String, genres: Array[String], year: Integer)

case class MovieWithSingleGenre(movieId: Long, title: String, genre: String, year: Integer)

case class MovieExploded(movieId: Long, title: String, genres: Array[String])

case class MovieAggregate(year: Int, count: Long)

import spark.implicits._ 

val source = spark.read
.option("header", true)
.option("inferSchema", true)
.csv("/home/dma/projects/hadoop-workshop/ml-latest/movies.csv")
.as[Movie]
.filter(_.title.matches("""^"?.*\(\d{4}\)\s*"?$"""))
.map(m => {
val lastOpen = m.title.lastIndexOf("(")
val year = m.title.substring(lastOpen + 1, lastOpen + 5).toInt
MovieWithYear(m.movieId, m.title.replaceAll("""\(\d{4}\)\s*"?$""", ""), m.genres, year)
})
.map(m => MovieWithGenresAndYear(m.movieId, m.title, m.genres.split("\\|"), m.year))
.flatMap(m => m.genres.map(g => MovieWithSingleGenre(m.movieId, m.title, g, m.year)))
.filter(_.genre != "(no genres listed)") 

%
source
.groupByKey(_.year)
.mapGroups((k, v) => (k, v.size))
.orderBy("_1")
.show() 

%spark
case class Rating(userId: Long, movieId: Long, rating: Double, timestamp: Long)

%spark
val ratings = spark.read
        .option("header", true)
.option("inferSchema", true)
.csv("/home/dma/projects/hadoop-workshop/ml-latest/ratings.csv")
.as[Rating]
.limit(10)
%spark

source.joinWith(ratings, source.col("movieId") === ratings.col("movieId"), "left")
        .filter(_._2 != null)
        .map {
            case (a, b) =>
                (a.title, b.rating)
        }
        .distinct()
        .limit(1)

%

```

### Victor Rentea – Integration Testing with Spring

*Rate*: 🌟 :star2: 🔥 :fire: 💪 :muscle: 🔁 :repeat:

*Links*:
* https://github.com/victorrentea/integration-testing-spring


### Алексей Нестеров - Spring Cloud в эру Kubernetes

*Rate*: 🌟 :star2: 🔥 :fire: 💪 :muscle: 🔁 :repeat:

*Feedback:* жизнь до и после кубернетис, `Spring Cloud` в помощь
* use `Kubernetes` для независимых от языка и стека базовых функций
* use `Spring Cloud` для тонкой настройки и контроля микросервисов

| Goal | Tools | Netflix | Spring Cloud | Kubernetes(K8s + Istio) |
| --- | --- | --- | --- | --- |
| Discovery | Service Discovery | Eureka | Eureka(or Consul/etcd/zookeeper) + Spring Cloud Discovery Client | K8S DNS |
| Fault tolerance | Circuit Breakers | Hystrix| Spring Cloud Circuit Breaker(Resilence4j, Hystrix ) | services + liveness / readiness |
| Resilience | Load Balancing | Ribbon(client-side load balancing) | Spring Cloud Load Balancer | Istio 'service mesh' |
| Configuration | Configuration | Archaius | Spring Cloud Config Server/Client | ConfigMap +  Secrets  |
| API management  | API gateways  | Zuul | Spring Cloud Gateway | Istio 'service mesh' |

Spring Cloud extra features:
* Tracing: Sleuth
* Event-based microservice: Spring CLud Stream
* Consumer Driven Contracts: Spring Cloud Contract
* FaaS:Spring Cloud Function
* REST clients: OpenFeign

Spring Cloud Integrations: 
* AWS
* Azure
* Google CLoud
* CloudFoundry
* Kubernetes


*Links*:
* https://github.com/alek-sys/spring-cloud-k8s-talk

# WATCH LATER

* Митя Александров – Helidon — Ласточка в мире микросервисов
* What I Wish I Knew About Maven Years Ago
* Константин Воливач: Обновление сложных сущностей без транзакций в распределенной системе
* Running Java Everywhere with GraalVM Native Image
* Олег Плисс – Преобразование приложений в нативно исполняемый образ в проекте GraalVM
* Grace Jansen – Reacting to an event-driven world
* Евгений Мандриков – Scala, Kotlin, Java и Code Coverage: показать все, что скрыто
* GraalVM: The one to rule them all

