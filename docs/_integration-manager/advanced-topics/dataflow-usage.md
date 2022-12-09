---
layout: default
title: DataFlow Job Configs
nav_order: 2
parent: Advanced Topics
---
# DataFlow Job Configs

## Overview

DataFlow applications can be configured, scheduled, and executed using Integration Manager if you have an active DataFlow license or subscription.

For convenience, DataFlow 8.0 is embedded within Integration Manager powered by DataCloud.

## How it Works

Integration Manager uses the dr command line interface to execute DataFlow applications. Before creating any DataFlow configurations, you should familiarize yourself with the dr interface concepts. You can learn more about these concepts at https://docs.actian.com/dataflow/7.0/#page/TroubleshootingRef%2FUsing_dr.htm%23.

Three DataFlow application types are supported:

* RushScript (.js)
* JSON Graph (.json)
* Java Application (.jar)

To learn more about creating DataFlow applications, see https://docs.actian.com/dataflow/8.0/.

## RushScript (.js) Setup

1. Create a new Job Config.
2. Upload your RushScript as the package (must have .js extension).
3. Optionally upload additional scripts or other files to the Files section, which will be injected using the "--includedir" command line option.
4. Optionally add entries to the Macros section, which will be injected using the "--variable" command line option. Note that the macro value text will be escaped accordingly when the command is constructed.
5. You can also take advantage of 2 special Integration Manager variables within your macro values:
    * $(LOCAL_JOB_SPEC_DIR) - This will resolve to the runtime working directory where your RushScript and additional files are located.
    * $(LOCAL_JOB_OUT_DIR) - This will resolve to the runtime output directory if you need to retrieve output files. Any files written to this location will be available at: {api_url}/jobs/{job-id}/out after the job has completed.

## JSON Graph (.json) Setup

1. Create a new Job Config.
2. Upload your Json Graph as the package (must have .json extension).
3. Optionally upload a properties file named "override.properties" to the Files section, which will be injected using the "--overridefile" command line option.
4. Optionally add entries to the Macros section, which will be injected using the "--override" command line option. Each macro can only override an operator within the graph, and MUST use the convention of MacroName=<operatorName.operatorProperty> and MacroValue=<overrideTextValue>. Note that the macro value   text will be escaped accordingly when the command is constructed.
5. You can also take advantage of 2 special Integration Manager variables within your macro values:
    * $(LOCAL_JOB_SPEC_DIR) - This will resolve to the runtime working directory where your RushScript and additional files are located.
    * $(LOCAL_JOB_OUT_DIR) - This will resolve to the runtime output directory if you need to retrieve output files. Any files written to this location will be available at: {api_url}/jobs/{job-id}/out after the job has completed.

## Java Application (.jar) Setup

1. Create a new Job Config.
2. Upload your Java Application .jar file as the package.
3. Type in the fully qualified main class within the jar as the entry point, e.g. com.foo.bar.MainClass, not MainClass.
4. Optionally add entries to the Macros section, which will be injected as an environment variable to the JVM. Note that the macro value text will be escaped accordingly when the command is constructed.

## Prerequisites

DataCloud subscribers have access to DataFlow out-of-box without additional configuration.

On-premise and VPC deployments of Integration Manager may require additional setup, see Server Admin > Dataflow Properties.