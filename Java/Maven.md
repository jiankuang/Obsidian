# Maven

## commands
`mvn [plugin]:[goal]` command format  
`mvn dependency:copy-dependencies` add dependencies to project(target/dependency)  
`mvn eclipse:eclipse` add dependencies to elipse(Referenced Libraries)  
`mvn compiler:compile` compiler plugin, compile goal  
`mvn compiler:compile -Dmaven.compiler.verbose=true` compile and get additional output  
`mvn compiler:help -Ddetail=true -Dgoal=compile` get the detail of compile goal  
`mvn clean` delete target directory  
`mvn clean install` multiple phases: delete target directory, then install 
`mvn help:describe -Dcmd=clean` describe clean phase  
`mvn help:describe -Dcmd=deploy` describe deploy phase  
`mvn help:describe -Dplugin=compiler` describe compiler plugin  
`mvn help:describe -Dcmd=compiler:compile -Ddetail` describe details of compile goal  
`mvn help:effective-pom`  see super pom  

## life cycles: default, clean, site
### default life cycle : include 23 phases(6 important phases)
  - validate: Not defined
  - initialize: Not defined
  - generate-sources: Not defined
  - process-sources: Not defined
  - generate-resources: Not defined
  - process-resources: org.apache.maven.plugins:maven-resources-plugin:2.6:resources
  - **compile: org.apache.maven.plugins:maven-compiler-plugin:3.1:compile**
  - process-classes: Not defined
  - generate-test-sources: Not defined
  - process-test-sources: Not defined
  - generate-test-resources: Not defined
  - process-test-resources: org.apache.maven.plugins:maven-resources-plugin:2.6:testResources
  - **test-compile: org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile**
  - process-test-classes: Not defined
  - **test: org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test**
  - prepare-package: Not defined
  - **package: org.apache.maven.plugins:maven-jar-plugin:2.4:jar**
  - pre-integration-test: Not defined
  - integration-test: Not defined
  - post-integration-test: Not defined
  - verify: Not defined
  - **install: org.apache.maven.plugins:maven-install-plugin:2.4:install**
  - **deploy: org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy**
   
### clean life cycle
* clean life cycle : include 3 phases
  - pre-clean
  - clean: org.apache.maven.plugins:maven-clean-plugin:2.5:clean ([plugin]:[goal])
  - post-clean

### site life cycle

## Plugins and Goals
example:
compiler plugin has 3 goals: compile, testCompile, help
### Customize the behavior of plugins (two ways)
`mvn compiler:compile -Dmaven.compiler.verbose=true` compile and get additional output  
```
<build>
	<pluginManagement>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven.compiler.plugin</artifactId>
				<version>3.2</version>
				<configuration>
					<verbose>true</verbose>
				</configuration>
			</plugin>
		</plugins>
	</pluginManagement>
</build>
```
