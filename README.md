# wix #
Experimentation with WiX - a software toolset that builds Windows Installer packages from XML code

## Table of contents ##
* [Installation](#installation)
* [Usage](#usage)
* [CI/CD Pipeline Integration](#ci_cd_pipeline_integration)
  * [Auto Harvesting](#auto_harvesting)

### Installation ###

### Usage ###

### CI/CD Pipeline Integration ###

#### Auto Harvesting ####
When your project contains many files to install, it can be quite cumbersome to create `File` and `Component` elements for all of them. Just imagine 

Instead, you can use a tool called `heat.exe`, wich ships with the WiX toolset. This tool can process a directory (usually it will be your build output directory) and create a separate .wxs file that contains a list of your application files. This file can be then refernced by your main Product.wxs script.

In a real project you would like to automatically harvest application files before every installer build. 
There are multiple ways to achieve it:

##### Run `heat.exe` manually #####

##### Use `HeatDirectory` task #####
The `HeatDirectory` task wraps heat.exe and can be built in your .wixproj script. 
If you generated your WiX project in Visual Studio, you'll find the following commented-out block in the very end of your .wixproject file:
```xml
<!--
To modify your build process, add your task inside one of the targets below and uncomment it.
Other similar extension points exist, see Wix.targets.
<Target Name="BeforeBuild">
</Target>
<Target Name="AfterBuild">
</Target>
-->
```
Just uncomment it and insert the following snippet into the `BeforeBuild` target:
```xml
<HeatDirectory Directory="RELATIVE_PATH_TO_DIRECTORY_TO_HARVEST"
               PreprocessorVariable="var.HarvestPath"
               OutputFile="OUTPUT_FILE_NAME"
               ComponentGroupName="COMPONENT_GROUP_NAME"
               DirectoryRefId="INSTALLFOLDER"
               AutogenerateGuids="True"
               ToolPath="$(WixToolPath)"
               SuppressFragments="True"
               SuppressRegistry="True"
               SuppressRootDirectory="True"/>
```
