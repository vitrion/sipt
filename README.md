# The Spark Image Processing Toolkit
The *Spark Image Processing Toolkit (SIPT)* is the easiest way to process grayscale digital image algorithms by using Apache Spark and the Hadoop Distributed File System (HDFS)

By using SIPT, you can distributedly process a large amount of images in a High Performance Computer System known as cluster. Alternativelly, you can use this software in both standalone and cluster mode in Spark. This software has been tested in Spark 2.3.1 and Hadoop 3.0.3.

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
   - Apache Spark(https://spark.apache.org/docs/latest/) and
   - Apache Hadoop(http://hadoop.apache.org/docs/r3.0.3/hadoop-project-dist/hadoop-common/SingleCluster.html)
3.  Assuming that both Spark and Hadoop are installed properly, download and unzip SIPT. You will be able to examine the output directory, where you will find:
   - The directory "./ImageSet" with some sample images, 
   - The JAR file "sipt_2.11-1.0.jar" that represents the SIPT toolkit and 
   - The file "SampleCode.scala."
4.  Open IntelliJ IDEA.
5.  Create a new Scala SBT Project.
## CSFL file description

| FILE NAME       | DESCRPTION |
| ---------       | ---------- |
| `cdev.h`          | This file provides the `cdev` class that manages the CUDA device properties |
| `fls.cuh`         | This is the main header file that the user must include in the applications. Provides the whole methods to manage fuzzy set objects of `fs` class, fuzzy variable objects of `fvar` class and fuzzy rule objects of `frule` class. Its functionality help the user to build fuzzy sets and systems. |
| `flsExcept.cuh`   | This file provides the fuzzy system object exceptions of `fls` class. |
| `flsFriends.cuh`  | This file provides the friend functions of `fls, fs, fvar` and `frule` classes. |
| `frule.cuh`       | This file provides the fuzzy rule class and its functionality based on STL objects of `string`class. |
| `fruleExcept.cuh` | This file provides the fuzzy rule object exceptions of `frule`class. |
| `fs.cuh`          | This file is the main building block for the `fls` class. Provides the fuzzy arithmetic and logic operations for fuzzy sets. Also it provides CUDA acceleration by enabling a flag called `isCUDA`. |
| `fsExcept.cuh`    | This file provides the fuzzy set object exceptions of `fs`. |
| `fvar.cuh`        | This file provides the fuzzy variable class and its functionality to contain and manage fuzzy set objects of `fs` class.                                                                                                               
| `fvarExcept.cuh`  | This file provides the fuzzy variable object exceptions of `fvar` class. |

## Basic CSFL methods to build fuzzy systems

| FLS METHOD | DESCRPTION |
| ---------- | ---------- |
| `fls::fls()` | Creates an initializes a fuzzy logic system. |
| `fls::seName(string name)` | Sets the `<name>` of the fuzzy logic system. |
| `fls::setInferenceModel(string model)` | Sets the inference `<model>` to Mamdani. |
| `fls::setHetProc(bool processing)` | Sets the `<processing>` type: false for sequential and true for heterogeneous by using CUDA. |
| `fls::setStream(bool processing)`  | Sets the `<CUDA Streams processing>` type: false for sequential and true for heterogeneous by using CUDA. |
| `fls::addFuzzyVar(string type, string name, vector<double> range)` | Adds a variable of <type> "Input" or "Output." The string called `<name>` establishes the name of the variable and the `<range>` is the interval of operation of the variable.                  |
| `fls::addFuzzySet(string variable, string name, string shape, vector<double> parameters, double normalization)` | Adds a fuzzy set called `<name>`, in a specific `<variable>`. Also, you can specify the `<shape>`, `<parameters>` and `<normalization>` values for each set. |
| `fls::addFuzzyRule(string)` | Adds a string-based fuzzy rule in a specific syntax and order. Each rule is included in the rule set ordered in the way it is added with this method. |
| `fls::configure()` | It builds the execution plan based on the current fuzzy system configuration by using the lazy evaluation of rules. Until here, no fuzzy rule has been executed, but an execution plan is ready for later execution. To execute the rule, use the `infer()` method. |
| `fls::fuzzify(vector<double> crisp_inputs)` | Fuzzify the crisp input values by using the Non-Singleton Fuzzification, according to the fuzzy system configuration.                                                                    |
| `fls::infer()` | Executes the inference machine according to the execution plan. An inferred set is obtained for each output variable. | 
| `fls::defuzzify()` | Returns the defuzzified value from the inferred set obtained with the method infer. The length of the resulting `std::vector` object that returns the `defuzzify()` method is defined by the number of the output variables. |
	
## Basic CSFL operators

|    OPERATOR     |             DESCRPTION                 |
|-----------------|----------------------------------------|
|        +        | Fuzzy arithmetic sum. Example: <ul><li> `fs A, B, C;` </li><li> `C = A + B;` </li></ul> |
|        -        | Fuzzy arithmetic subtraction. Example: <ul><li> `fs A, B, C;` </li><li> `C = A - B;` </li></ul> |
|        *        | Fuzzy arithmetic product. Example: <ul><li> `fs A, B, C;` </li><li> `C = A * B;` </li></ul> |
|        /        | Fuzzy arithmetic division. Example: <ul><li> `fs A, B, C;` </li><li> `C = A / B;` </li></ul> |
|        &        | Fuzzy logic intersection. Example: <ul><li> `fs A, B, C;` </li><li> `C = A & B;` </ul> |
|        <code>&#124;</code>        | Fuzzy logic union. Example: <ul><li> `fs A, B, C;` </li><li> <code> C = A &#124; B;</code> </li></ul> |
|        !        | Fuzzy logic complement. Example: <ul><li> `fs A, B;` </li><li> `B = !A;` </li></ul> |

## Building your own application

Once you have installed all the required programs for the CSFL v1.1, please write the following code to build a simple Fuzzy System for the DC Servomotor Control. This example is expressed as a pseudo-code in the derived paper:
```
// The number of samples defines the vector operations length
extern const unsigned int samples(100000);
// To start building CUDA-accelerated fuzzy systems import the library
#include "fls.cuh"

int main()
{
	float pi = acos(-1);
	
	// This creates the CUDA information needed for operation
	CUDAinit();
	// These are the crisp input observations
	float e = -pi / 2;
	float c = pi / 6;
	// The sigma value is needed to build non-singleton sets for fuzzification
	float e_sigma = pi / 10;
	float c_sigma = pi / 30;
	// These flags determine the execution mode
	bool isCUDA = true;
	bool isStream = true;

	// Here the fls constructor defines the execution mode
	fls motor(isCUDA, isStream);

	// Set the fuzzy system application name
	motor.setName("Servomotor");
	// Set the inference model
	motor.setInferenceModel("Mamdani");

	// Set the variable ranges and names
	vector<float> range1 = { -pi / 2, pi / 2 };
	vector<float> range2 = { -pi / 6, pi / 6 };
	string name1 = "Error";
	string name2 = "Change";

	// Linguistic variable error has been created
	motor.addFuzzyVar("Input", name1, range1[0], range1[1]);
	// Linguistic variable change has been created
	motor.addFuzzyVar("Input", name2, range2[0], range2[1]);
	// Linguistic variable voltage has been created
	motor.addFuzzyVar("Output", "Voltage", -7.5, 7.5);
	
	//Three linguistic terms have been created for the error
	motor.addFuzzySet("Error", "Negative", "Z", { -pi / 2, 0 }, 1);
	motor.addFuzzySet("Error", "Zero", "Triangular", { -pi / 2, 0, pi / 2 }, 1);
	motor.addFuzzySet("Error", "Positive", "S", { 0, pi / 2 }, 1);
	//Three linguistic terms have been created for the change
	motor.addFuzzySet("Change", "Negative", "Z", { -pi / 6, 0 }, 1);
	motor.addFuzzySet("Change", "Zero", "Triangular", { -pi / 6, 0, pi / 6 }, 1);
	motor.addFuzzySet("Change", "Positive", "S", { 0, pi / 6 }, 1);
	//Three linguistic terms have been created for the voltage
	motor.addFuzzySet("Voltage", "Negative", "Z", { -5, 0 }, 1);
	motor.addFuzzySet("Voltage", "Zero", "Triangular", { -5, 0, 5 }, 1);
	motor.addFuzzySet("Voltage", "Positive", "S", { 0, 5 }, 1);

	// Rule set is comprised of 9 rules
	motor.addFuzzyRule("(Error: Negative) AND (Change: Negative) THEN (Voltage: Negative)");
	motor.addFuzzyRule("(Error: Negative) AND (Change: Zero) THEN (Voltage: Negative)");
	motor.addFuzzyRule("(Error: Negative) AND (Change: Positive) THEN (Voltage: Negative)");
	motor.addFuzzyRule("(Error: Zero) AND (Change: Negative) THEN (Voltage: Negative)");
	motor.addFuzzyRule("(Error: Zero) AND (Change: Zero) THEN (Voltage: Zero)");
	motor.addFuzzyRule("(Error: Zero) AND (Change: Positive) THEN (Voltage: Positive)");
	motor.addFuzzyRule("(Error: Positive) AND (Change: Negative) THEN (Voltage: Positive)");
	motor.addFuzzyRule("(Error: Positive) AND (Change: Zero) THEN (Voltage: Positive)");
	motor.addFuzzyRule("(Error: Positive) AND (Change: Positive) THEN (Voltage: Positive)");

	// Here, the execution plan is lazily evaluated and the fuzzy system is ready for making decisions
	motor.configure();
	
	// The non-singleton fuzzy observations have been created
	fs a(range1[0], range1[1], 1.0, name1 + "_prime", "Gaussian", { e, e_sigma }, true, true);
	fs b(range2[0], range2[1], 1.0, name2 + "_prime", "Gaussian", { c, c_sigma }, true, true);

	// Fuzzify by using the non-singleton fuzzy observations
	motor.fuzzify({ a, b });
	// Perform the inference process according to the execution plan
	motor.infer();
	// Defuzzify the implied set of voltage
	vector<float> result = motor.defuzzify();
	cout << "The inferred voltage generated from inputs " << e << "(rads) and " << c << "(rads/s) is " << result[0] << " volts.";
	// his deletes all the CUDA information used during operation
	CUDAend();

	cin.get();
    return 0;
}

```
