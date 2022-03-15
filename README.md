# ada-to-uppaal
An EMF based Ada to Uppaal converter

Introduction
============

For my graduation project I made a tool to generate an indermediate representation for Ada code, see: https://github.com/jildert17/happyflow-extractor

This repository provides the tools to convert the intermediate Ada representation into an Uppaal model in order to eventually perform model checking on the original source code.
This conversion is done in two steps: 1) a model-to-model conversion and 2) a model-to-text conversion. The textual output is a file which can be opened by the Uppaal application.

This repository provides a meta model for the Ada programming language, to be used in the Eclipse Modelling Framework (EMF), and a model-to-model transformation from the given Ada (meta) model to an Uppaal meta model. The transformation is written in the ETL language (https://www.eclipse.org/epsilon/doc/etl/).

The Uppaal meta model can be found here: https://github.com/egbertpostma/uppaal/tree/master/metamodel/org.muml.uppaal/model

The Uppaal model-to-text transformation definition can be found here: 

Setup
=====

Model-to-model conversion
-------------------------

To perform the first step, the model-to-model conversion, an Eclipse project should be created. Within this project a Run Configuration should be added. The run configuration should be of type 'ETL Transformation'.

As the 'Source' of this transformation, the \*.ETL file (provided in this repo) should be given.

In the models tab of the run configuration two models should be added, an input model and an output model. A run configuration is added to the repo (Ada2Uppaal.launch), but it can also be added manually by applying below steps.

The input model should have the following info:
* Name: In
* Model file: the file containing the intermediate Ada represenation
* Metamodel: the Ada metamodel provided in this repo
* 'Read on load': Checked
* 'Store on disposal': Unchecked

The output model should have the following info:
* Name: Out
* Model file: The name of the Uppaal model to be generated
* Metamodels: the Uppaal metamodel
* * 'Read on load': Unchecked
* 'Store on disposal': Checked

Model-to-text conversion
--------------------------

This step also requires a Run Configuration in Eclipse. This time the source model is the generated Uppaal model from the previous step, and the output is an Uppaal text file.

The model-to-text definition is given in uppaal2xsd.etl and the Uppaal-text 'metamodel' is the 'upaal.xsd' file. Both should be or have been on this location:
https://github.com/fraunhofer-iem/uppaal-model
