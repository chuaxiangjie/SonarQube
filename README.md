# SonarQube with .Net Core

Provide Code analysis and integration with NUnit

## Getting Started

These instructions will get you a copy of the software and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them

#### Windows Environment

1. Install latest SonarQube Community Edition
(https://www.sonarqube.org/success-download-community-edition/)

2. Install latest .Net 5 SDK (Skip if already installed)

3. Download OpenJDK 11
(https://download.java.net/java/ga/jdk11/openjdk-11_windows-x64_bin.zip) 

Sonarqube works only with JDK 11

4. Specify JAVA_HOME environment variable

<img src="https://user-images.githubusercontent.com/5947398/102429364-7f758600-404d-11eb-928d-05c94404037a.png" width="600" />

5. Start Sonarqube

<img src="https://user-images.githubusercontent.com/5947398/102431545-10e4f800-404e-11eb-8b08-f9cda1842281.png" width="600" />

```
#### Windows Cli

cd C:\Users\ran_d\Downloads\sonarqube-8.5.1.38104\sonarqube-8.5.1.38104\bin\windows-x86-64

StartSonar.bat

```

6. Launch Sonarqube http://localhost:9000



## Sonarqube project (Setup)

#### Create new project

<img src="https://user-images.githubusercontent.com/5947398/102434521-e1cf8600-404f-11eb-9018-fffaa5a3a284.png" width="600" />

<img src="https://user-images.githubusercontent.com/5947398/102435354-6b338800-4051-11eb-80fc-7878e645f51a.png" width="600" />


#### Install Global MSBuild scanner

http://localhost:9000/documentation/analysis/scan/sonarscanner-for-msbuild/

```
#### Installation of the SonarScanner for MSBuild .NET Core Global Tool

dotnet tool install --global dotnet-sonarscanner --version 4.8.0

```


## Sonarqube project (Scan)

#### Scan .Net project



```diff
#### Navigate to .Net project root directory


dotnet sonarscanner begin /k:"NumberGenerator" /d:sonar.cs.nunit.reportsPaths=C:\Users\ran_d\source\repos\NumberGenerationNew\Tests\**\TestResults\TestResults.xml /d:sonar.cs.opencover.reportsPaths=C:\Users\ran_d\source\repos\NumberGenerationNew\Tests\**\Coverage\*.opencover.xml


Parameters explain
- /k:"NumberGenerator" - refer to sonarqube project name
- /d:sonar.cs.nunit.reportsPaths - specify Nunit unit tests result
- /d:sonar.cs.opencover.reportsPaths - specify Nunit unit tests coverage

```

```
#### Build solution

dotnet build NumberGenerator.sln

```


```
#### Execute test to generate test results/coverage files

dotnet test --logger "trx;LogFileName=TestResults.trx" ^            --logger "nunit;LogFileName=TestResults.xml" ^            --results-directory ./Coverage ^            /p:CollectCoverage=true ^            /p:CoverletOutput=Coverage\ ^            /p:CoverletOutputFormat=opencover ^            /p:Exclude="[nunit.*]*

```

```
#### Sonarscan end

dotnet sonarscanner end

```
