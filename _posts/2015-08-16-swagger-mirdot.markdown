---
layout:     post
title:      "Swagger, Miredot - API documenting tools"
subtitle:   "Swagger,Miredot"
date:       2015-10-12 12:00:00
author:     Sriram Mantha
---

## API Documentation

Its always a challenge keep your API well documented. To get changes out the door developers always make quick changes api's and the ship them out failing to update API documents


## Swagger

Swagger provides open source libs/tools for generating docs for API's, Client Side SDK generation and dicoverability

### Generating swagger.json from your existing code base

Import Swagger core lib

```
<dependency>
      <groupId>com.wordnik</groupId>
      <artifactId>swagger-core</artifactId>
      <scope>compile</scope>
      <version>1.5.1-M2</version>
      <exclusions>
        <exclusion>
          <groupId>javax.ws.rs</groupId>
          <artifactId>jsr311-api</artifactId>
        </exclusion>
      </exclusions>
</dependency>
```

Here is a useful maven plugin developed by that can be used to generate the swagger.json from your existing source code.
The following plugin parses swagger annotation to generate a swagger json. Here is the [github repo](https://github.com/kongchen/swagger-maven-plugin)
The swagger.json can be fed to a swagger ui which neatly displays the API's details in a nice UI.

```
<plugin>
        <groupId>com.github.kongchen</groupId>
        <artifactId>swagger-maven-plugin</artifactId>
        <version>3.0.0</version>
        <configuration>
          <apiSources>
            <apiSource>
              <locations>com.mysaas.resource</locations>
              <schemes>http,https</schemes>
              <host>localhost:8080</host>
              <basePath>/api</basePath>
              <info>
                <title>Swagger Maven Plugin Sample</title>
                <version>v1</version>
                <!-- use markdown here because I'm using markdown for output, if 
                  you need to use html or other markup language, you need to use your target 
                  language, and note escape your description for xml -->
                <description>
                  This is a sample.
                </description>
              </info>
              <!-- Support classpath or file absolute path here. 1) classpath e.g: 
                "classpath:/markdown.hbs", "classpath:/templates/hello.html" 2) file e.g: 
                "${basedir}/src/main/resources/markdown.hbs", "${basedir}/src/main/resources/template/hello.html" -->
              <templatePath>${basedir}/src/test/resources/strapdown.html.hbs</templatePath>
              <outputPath>${basedir}/generated/document.html</outputPath>
              <swaggerDirectory>${basedir}/generated/swagger-ui</swaggerDirectory>
            </apiSource>
          </apiSources>
        </configuration>
        <executions>
          <execution>
            <phase>compile</phase>
            <goals>
              <goal>generate</goal>
            </goals>
          </execution>
        </executions>
</plugin>
```

### Swagger UI

Swagger resource definition file can be used to generate Client stubs.
Here is the github [link ](https://github.com/swagger-api/swagger-codegen)

## MireDot

Basic docs can be generated using Miredot with it free version. Here is the [link](http://miredot.com/docs/getting-started/#)
You will need to regsiter to get the license key which is based on the artifact Id. You will need to generate a new one when the maven artifact changes


