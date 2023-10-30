<div id="top"></div>


<!-- PROJECT LOGO -->
<br />
<div align="center">
    <img src="image/sparklogo.jpg" alt="Logo" width="500" height="400">
  
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
        <li><a href="#introduction">Introduction</a></li>
        <li><a href="#objectifs">Objectifs</a></li>
        <li><a href="#code_et_outputs">Code et Outputs</a></li>
       
  </ol>
</details>

- # [Introduction](#Introduction)

Spark SQL est un élément clé du framework Apache Spark, fournissant une interface SQL pour l'analyse et la manipulation de grandes quantités de données. Elle facilite la gestion de grands ensembles de données en permettant aux utilisateurs de travailler avec des données structurées et semi-structurées en utilisant des requêtes SQL. Spark SQL peut interagir avec plusieurs sources de données, telles que Hive, Parquet et JSON, et bénéficie d'optimisations de performance pour traiter efficacement les données sur des clusters distribués. Que vous soyez un ingénieur en données, un scientifique des données ou un développeur, Spark SQL facilite la manipulation et l'analyse de grandes quantités de données, aidant ainsi à extraire efficacement des informations précieuses de vos données. 

- # [Objectifs](#Objectifs)
L'objectif principal de cette première section est de présenter les bases de Spark SQL en mettant en avant son abstraction de base, ses opérations structurées de manipulation de données et les différentes sources de données prises en charge pour la lecture et l'écriture. L'apprentissage de la création de DataFrames par transformation d'un RDD, programmation ou chargement de données de sources externes est l'un des objectifs spécifiques. De plus, il vise à familiariser les participants avec l'utilisation de l'API DataFrame pour des tâches telles que la sélection, le filtrage, le tri et le regroupement de données, l'application de fonctions SQL sur les DataFrames, la conversion des DataFrames en RDD et l'enregistrement des données dans des sources externes.Enfin, cette section présente un aperçu des DataSets qui ont été introduits avec Spark 1.6. Il explique également comment créer des DataFrames à partir de requêtes SQL et comment exécuter ces requêtes sur les données DataFrame. Pour une compréhension approfondie de ces concepts, une connaissance de base de SQL est recommandée.

  
- # [Code et Outputs](#code_et_outputs)
   ## Librairies:
  ```scala
import org.apache.spark.sql.functions.{col, count, lit}
import org.apache.spark.sql.types.StructType
import org.apache.spark.sql.{Column, DataFrame, Dataset, Row, SparkSession, functions}
import org.apache.spark.sql.types.{BooleanType, LongType, StringType, StructField, StructType}

import scala.collection.immutable.BitSet.empty
import scala.collection.immutable.Seq
  def getConfiguration(): SparkSession = {
    val spark = SparkSession.builder().appName("SparkApp3_Scala").master("local[*]").getOrCreate()
    spark
  }```


# Création des Dataframes:
  ## Création par différentes méthodes:
```scala
  def createDF_fromSeq(spark: SparkSession): DataFrame = {
    import spark.implicits._
    val sc = spark.sparkContext
    val data = Seq(("1", "Jad", "20"), ("2", "Tim", "19"), ("3", "Nicola", "18"))
    val etudRDD = sc.parallelize(data)
    val df = etudRDD.toDF("ID", "Name", "Age")  // Nommez les colonnes ici
    df
  }

  def createDF_fromSeq_V2(spark: SparkSession): DataFrame = {
    import spark.implicits._
    val sc = spark.sparkContext
    val data = Seq((1L, "Jad", 20L), (2L, "Tim", 19L), (3L, "Nicola", 18L))
    val etudRDD = sc.parallelize(data)
    val df = etudRDD.toDF("ID", "Name", "Age")  // Nommez les colonnes ici et définissez les types de données
    df
  }
  def createDF_byRow(spark: SparkSession) : DataFrame = {
    val sc = spark.sparkContext
    val etudRDD = sc.parallelize(List(Row(1L, "Jad", 20L), Row(2L, "Tim", 19L), Row(3L, "Nicola", 18L)))
    val schema = StructType(Array(StructField("ID", LongType,true), StructField("Name", StringType, true),StructField("Age", LongType, true)))
    val etudDF = spark.createDataFrame(etudRDD,schema)
    return etudDF
  }

  //------------------Création à partir d’un fichier CSV

  def createDF_CSV(spark: SparkSession, path: String): DataFrame = {
    //val movies = spark.read.option("header","true").csv(path)
    val movieSchema = StructType(Array(StructField("actor_name", StringType,
      true), StructField("movie_title", StringType, true), StructField("produced_year",
      LongType, true)))
    val moviesDF = spark.read.options(Map("header" -> "true", "delimiter" -> ","
      , "inferschema" -> "true")).schema(movieSchema).csv(path)
    return moviesDF
  }
//-----------------Création à partir d’un fichier JSON
 def createDF_JSON(spark: SparkSession, path: String): DataFrame = {
    val movieSchema = StructType(Array(StructField("actor_name", StringType, true),
    StructField("movie_title", StringType, true), StructField("produced_year",
      BooleanType, true)))
  val moviesDF = spark.read.schema(movieSchema).option("inferSchema","true")
    .option("mode","failFast").json(path)
  return moviesDF
}
  /*def createDF_DB(spark: SparkSession): DataFrame = {
    val mysqlURL = "jdbc:mariadb://127.0.0.1:3305/movies"
    val filmDF =
      spark.read.format("jdbc").option("driver","org.mariadb.jdbc.Driver")
        .option("url", mysqlURL).option("dbtable", "movie").option("user", "root")
        .option("password", "admin").load()
    return filmDF}
```
<p align="center">
     <img src="image/to do app.png">
   </p>


```scala

``````scala

``````scala

``````scala

```

 <!-- PROJECT LOGO -->
<br />
<div align="center">
    <img src="image/adddialog ui.png" alt="Logo" width="500" height="400">
  
</div>





Our Team -[DARBAL nour-elhouda](https://github.com/teamkhaoulanour) .

Project Link: [Spark-sql](https://https://github.com/Darbal-Nour-elhouda/Spark-sql/new/main](https://github.com/Darbal-Nour-elhouda/Spark-sql/edit/main/README.md#Introduction))

Encadré par : [Mr.IMADEDDINE MOUNTASSER](https://)


<p align="right">(<a href="#top">back to top</a>)</p>
