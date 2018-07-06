# The Spark Image Processing Toolkit
The *Spark Image Processing Toolkit (SIPT)* is the easiest way to process grayscale digital image algorithms by using Apache Spark and the Hadoop Distributed File System (HDFS)

By using SIPT, you can distributedly process a large amount of images in a High Performance Computer System known as cluster. Alternatively, you can use this software in both standalone and cluster mode in Spark. This software has been tested in Spark 2.3.1 and Hadoop 3.0.3.

## How to cite this software

This software was developed under the sponsory of the Mexican Council for Science and Technology under project number 1170.
A journal article is derived from this software, which can be cited by the user as follows:

Téllez‐Velázquez A, Cruz‐Barbosa R. A *Spark image processing toolkit.* Concurrency Computat Pract Exper. 2018; Under review

## Contact information

For further information about installing this software, please send us an email to the following recipients:

Dr. Arturo Téllez-Velázquez
atellezve@conacyt.mx

Dr. Raúl Cruz-Barbosa
rcruz@mixteco.utm.mx

UNIVERSIDAD TECNOLÓGICA DE LA MIXTECA
Carretera a Acatlima km. 2.5, Zip. Code 69000,
Huajuapan de León, Oaxaca, México, 2016.
Phone number: +52 953 532 0399 ext. 200.

## System requirements
1.  A cluster computing system (master - single node, master - several nodes). If you do not have a cluster available, you can test this software in a personal computer.
2.  Linux operating system
3.  OpenJDK version 8
4.  Spark 2.3.1
5.  Hadoop 3.0.3
6.  Jetbrains IntelliJ IDEA
7.  Any image viewer

## Instalation guidelines

Guidelines for installing the SIPT v1.0:

1.  Assuming that the OpenJDK is installed, download the software from the following repositories:
      - Apache Spark (https://www.apache.org/dyn/closer.lua/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz) and
      - Apache Hadoop (http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.0.3/hadoop-3.0.3.tar.gz)
2.  Install Spark and Hadoop according to the developer's webpage: 
      - Apache Spark (https://spark.apache.org/docs/latest/) and
      - Apache Hadoop (http://hadoop.apache.org/docs/r3.0.3/hadoop-project-dist/hadoop-common/SingleCluster.html)
3.  Assuming that both Spark and Hadoop are installed properly, download and unzip the "sipt_v1.0.zip" file in your home directory. You will be able to examine the output directory `~/sipt_v1.0/`, where you will find:
      - The directory "./ImageSet" with some sample images, 
      - The JAR file "sipt_2.11-1.0.jar" that represents the SIPT toolkit,
      - The file "SampleCode.scala" and
      - The file "build.sbt"
4.  Open IntelliJ IDEA.
5.  Create a new Scala SBT Project providing the following information:
      - Name: SampleCode
      - Location: `~/IdeaProjects/SampleCode`
      - JDK: IMPORTANT!!! JDK 8 is a due. If JDK is properly installed, you will see the JDK version here, e.g. 1.8 (Java version 1.8.X.XXX). Is you installed IntelliJ IDEA with JDK included, you will not need to browse the available JDK installations.
      - SBT: Do not change this option. In most cases, the default Scala Build Tool (SBT) version fits with SIPT.
      - Scala: IMPORTANT!!! Please be sure to specify the supported Scala version that fits with Spark, i.e. Scala 2.11.8.
      - Finish. Whenever the above information is complete, you can press the Finish button.
6.  Replace the "build.sbt" file in project's directory `~/IdeaProjects/SampleCode` with the "build.sbt" file obtained from the extracted file in `~/sipt_v1.0/build.sbt`. Open the SBT file and replace the "vitrion" usarename for your username in line 12.
7.  Refresh the project by using the new "build.sbt" file. Also, wait until IntelliJ IDEA finishes to install the required software from the download Maven's repositories. After the project is updated, you will be able to use the imported SIPT packages. 
8.  Copy the "SampleCode.scala" file in the project's directory `~/IdeaProjects/SampleCode/src/main/scala/SampleCode.scala`. You will be able to see and open the file from the Project Structure. If no Scala SDK is installed, you will be asked to select the appropriated Scala version. Please ensure that the Scala version 2.11.8 is selected.
9.  Open the "SampleCode.scala" file and replace the "vitrion" username for your username in both lines 13 and 15. Notice that the "InputPath" value addresses the directory where the input image set is stored and "OutputPath" value addresses the directory where the output image set will be stored.
12.  Open the SBT Shell and wait until the project has been updated.
13.  Then type in the SBT Shell the command `package` and wait until the compilation and packaging have finished.
14.  Go to the `~/IdeaProjects/SampleCode/target/scala-2.11/` directory and type in the terminal the command `spark-submit --jars ~/sipt_v1.0/sipt_2.11-1.0.jar samplecode_2.11-1.0.jar`.
15.  Go to your home directory and you will find a new subdirectory named as SIPT, i.e. `~/sipt/`. Here you will find the resulting image set after applying the image operation that you specified in the "SampleCode.scala" file.

This is just a sample application that can be used in future implementations where you want to used SIPT as your main distributed image processing tool. As can be seen in this sample tutorial, with SIPT you can import, read, write, export and process a large amount of digital grayscale images, by taking advantage of a cluster architecture, Apache Spark and the Hadoop Distributed File System.

As future work is expected to expand the compatible image file formats, include more-than-the-available image processing algorithms and even extend them to digital color images.
