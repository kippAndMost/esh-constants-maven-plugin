# ESH Constants Generator Maven Plugin

![Main Workflow State](https://github.com/kokuwaio/esh-constants-maven-plugin/workflows/Main/badge.svg)

## What?

This plugin generates a Java constants class with all namings defined in the `ESH_INF` folder files.

## Why?

Because it's hard to write this class on your own, if you have a lot of content. Also, the XML files should be
in the lead and your code base is in sync all the time.

## How?

The plugin scans for all XML files in the given input directory. It parses every file (DOM parsing, so do not put
extremely large files there) and looks for the nodes listed below. The text content of those matching nodes are
collected and put together to a Java constant class.

| Constant Type         | XPath                           | Constant Prefix        | Description                    |
|-----------------------|---------------------------------|------------------------|--------------------------------|
| Binding ID            | //thing-descriptions/@bindingId | BINDING_ID_            | The ID of the binding          |
| Thing Type ID         | //thing-type/@id                | THING_TYPE_ID_         | The ID of a thing type         |
| Bridge Type ID        | //bridge-type/@id               | BRIDGE_TYPE_ID_        | The ID of a bridge type        |
| Channel ID            | //channel/@id                   | CHANNEL_ID_            | The ID of a channel            |
| Channel Type ID       | //channel-type/@id              | CHANNEL_TYPE_ID_       | The ID of a channel type       |
| Channel Group Type ID | //channel-group-type/@id        | CHANNEL_GROUP_TYPE_ID_ | The ID of a channel group type |
| Channel Group ID      | //channel-group/@id             | GID_                   | The ID of a channel group      |

## Usage

Plugin Goals:

| Goal                   | Default Phase    | Description                        |
|------------------------|------------------|------------------------------------|
| generate-esh-constants | generate-sources | Generates the constants Java class |

Plugin Configuration:

| Configuration   | Default Value              | Description       |
|-----------------|----------------------------|-------------------|
| packageName     | -                          | Java package name |
| className       | -                          | Java class name   |
| inputDirectory  | src/main/resources/ESH-INF | Input directory   |
| outputDirectory | target/generated-sources   | Output directory  |

Example:

```xml
<plugins>
	<plugin>
		<groupId>io.kokuwa.edge</groupId>
		<artifactId>esh-constants-maven-plugin</artifactId>
		<version>RELEASE</version>
		<executions>
			<execution>
				<id>generate-esh-constants</id>
				<goals>
					<goal>generate-esh-constants</goal>
				</goals>
				<phase>generate-sources</phase>
				<configuration>
					<packageName>io.kokuwa.examples</packageName>
					<className>Constants</className>
					<inputDirectory>${project.basedir}/src/main/resources/ESH-INF</inputDirectory>
					<outputDirectory>${project.build.directory}/generated-sources</outputDirectory>
				</configuration>
			</execution>
		</executions>
	</plugin>
</plugins>
```

## Contribution

Feel free to add every missing constant XPath as a pull request or kick off an issue on every trouble.

## TODOs

* Generate all UIDs
* Generate channel group association
* Generate XMLs / Constants (even parts of handler?) form OpenAPI file
