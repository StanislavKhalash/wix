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
When your project contains many files to install, it can be quite cumbersome to create `File` and `Component` elements for all of them. Instead, you can use a tool called `heat.exe`, wich ships with the WiX toolset.
In a real project you would like to automatically harvest application files before building an installer. There are multiple ways to achieve it.

##### Run `heat.exe` manually #####

##### Use `HeatDirectory` task #####
The `HeatDirectory` task wraps heat.exe and can be built in your .wixproj script. 
If you generated your WiX project in Visual Studio, you'll find the following commented-out block in the very end of your .wixproject file.
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
