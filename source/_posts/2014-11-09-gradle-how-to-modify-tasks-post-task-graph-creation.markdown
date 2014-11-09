---
layout: post
title: "Gradle : How to modify tasks post task graph creation"
date: 2014-11-09 02:16:28 -0500
comments: true
categories: 
---

Gradle allows you to script your build file and add hooks in to the build lifecycle so you can maximize flexibility without compilcating build setup and tasks.
One of the useful ways to manipulate all tasks once they are loaded by gradle into task execution graph is to use the whenReady lifecycle hook which gets called when gradle populates the complete tasks execution graph.This also allows you to dynamically modify task properties, add new properties,etc. This comes helpful when you need to manipulate some tasks based on the user arguments passed in the project.

Below is the snippet that you need to add tomake this work:
gradle.taskGraph.whenReady {
  tasks.each {
    it.doFirst { 
      println "Calling ${it.name}"
    }
  }
}

Output:
sgokak@sgokak-ThinkPad-T430 ~/myspace/gradle-in-action/Todo $ gradle build
:compileJava
Calling compileJava
:processResources UP-TO-DATE
:classes
Calling classes
:war
Calling war
:assemble
Calling assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses
Calling testClasses
:test UP-TO-DATE
:check
Calling check
:build
Calling build

BUILD SUCCESSFUL

Total time: 10.185 sec
