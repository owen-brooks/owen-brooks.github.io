---
layout: post
title:  "Using External Jars With Maven"
date:   2018-06-29 10:34:25
categories: Maven Java Build 
tags: featured
image: /assets/article_images/Podcasts/headphones.jpg
---
Maven is a great tool. It makes managing dependencies, packaging and deployment extremely easy. Maven relies on a pom.xml file in order to work. Users include dependencies in this file and maven pulls the jars from its public repository. These dependencies can also be adapted to use private / third-party repositories. The problem comes when you want to use an external jar that is not already in a repository. I will explore two solutions, detailing how to get around this.

# Option 1: Deploy the jar your local repository

This option is good for jars that you do not want released / available to other people. This comes into play when using purchased software that you do not have the legal rights to distribute. This does however, increase the size of your project as jars will need to be stored with your project files.
Steps:
First create the folder “repo” in the root directory of your project. Place your jar in that folder.

Add the following code in your pom.xml file under the dependencies tags. Change jarNAme to match your jar. The groupId and version does not really matter in a local repository as long as they are there. Maven will place the jar at the following path **/groupId/artifactId/version/artifactId-version.jar**

{% highlight xml %}

<dependency>
    <groupId>example</groupId>
	<artifactId>jarName</artifactId>
	<version>1.0</version> <!-- Dummy Version -->
	<scope>system</scope>
	<systemPath>${project.basedir}/repo/jarName.jar</systemPath>
</dependency>

{% endhighlight %}

Run maven with goals clean build. Your jar will be added to your local repository and your project should build.

# Option 2: Add jar to public repository

This is probably the more standard approach, as it allows others to use the jars you have deployed. As long as you have credentials to post to the repository, it can be as simple as the first option. If you or your company does not have a repository in place you can create a simple one using GitHub. Good directions for that can be found here : https://stackoverflow.com/a/16429851
If your company is looking to create a nexus repospitory a good guide can be found [here](http://blog.arungupta.me/setup-local-nexus-repository-deploying-war-from-maven-techtip74/)
You can then push the jar to the repository using this [tutorial by sonatype](https://blog.sonatype.com/2008/11/adding-a-jar-to-a-maven-repository-with-sonatype-nexus/).


