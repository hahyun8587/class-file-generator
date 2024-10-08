# ClassFileGenerator

ClassFileGenerator is simple program that generates Java Virtual Machine (JVM)  
class files. It takes root input directory that contains formatted Json files  
as an argument and saves desired class files to output directory.  

</br>

## 1. Requirements

</br>

## 2. Building

ClassFileGenerator uses Maven to build the project.  

```console
mvn install
```

</br>

## 3. Environment Setting

ClassFileGenerator uses script to run the application. Path to the script  
needs to be appended to environment variable `Path` in order to execute the  
script in any location. Additionally, path to the local maven repository need  
to be set to environment variable `MAVEN_LOCAL` in order to execute the script.

### Linux:

The following command sets environment variables temporally. To set them  
permanently, type the command to `~/.bashrc`.

```bash
PATH=$PATH:path/to/class-file-generator/scripts

export MAVEN_LOCAL=path/to/maven/local/repo
```

### Windows:

The following command sets environment variables permanently.

```powershell
[Environment]::SetEnvironmentVariable('PATH', [Environment]::GetEnvironmentVariable('PATH', 'Machine') + ';path\to\class-file-generator\scripts', 'Machine')

[Environment]::SetEnvironmentVariable('MAVEN_LOCAL', 'path\to\maven\local\repo', 'Machine')
```

</br>

## 4. Usage

After [building](#2-building) and  
[setting environment](#3-environment-setting), run the application with the  
following command.

```console
cfg [options] path_to_root_input_directory
```

`path_to_root_source_directory` denotes absolute or relative path of the root  
input directory.

### Options

- -d, --directory <output_directory>: Set output directory. <output_directory>  
can be both absolute and relative path of the output directory. If this option  
is not specified, output class files are saved in `~/class-files`.

- -h, --help: Print help message.

</br>

## 5. Json File Format

Json files in the root input directory must follow the following format.

```json
{
    "packagename": "package name",
    "classname": "class name",
    "methodname": "method name",
    "methodDesc": "method description",
    "byteStrings": ["hex string 1", "hex string 2"]
}

```

### Example

The following json file generates class file that represents the following  
java source code.

### Json File

```json
{
    "packagename": "edu.handong.csee.isel.cfg.gen",
    "classname": "Add", 
    "methodname": "add",
    "methodDesc": "(II)I",
    "byteStrings": ["1B", "1C", "60", "AC"]
}

```

### Java Source Code

```java
package edu.handong.csee.isel.cfg.gen;

public class Add {

    public int add(int a, int b) {
        return a + b;
    }
}

```

Since ClassFileGenerator is designed to generate class files  
from bytecode instructions generated by AlphaByte, it does not utilize constant  
pool. Therefore, generated class files do not have field and have only one  
solution method. Also, body of the method only have bytecode instructions that  
do not utilize constant pool.
