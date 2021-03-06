---
layout: post
title:  "QueryDSL 관련 pom.xml 오류"
date:   2018-10-11 22:00:02
categories: [JPA]
tags: [JPA,QueryDSL]
comments: true
---
이클립스에서 QueryDSL로 생성한 Q도메인들을 인식하지 못하여 원인을 파악해보니 pom.xml 의 플러그인 설정에 다음과 같은 오류가 나고 있었다.
<!--more-->
{% highlight xml %}
<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-dependency-plugin</artifactId>
		<version>2.4</version>
		<executions>
				<execution>
						<id>copy-dependencies</id>
						<phase>package</phase>
						<goals>
								<goal>copy-dependencies</goal>
						</goals>
				</execution>
		</executions>
</plugin>
{% endhighlight %}

You need to run build with JDK or have tools.jar on the classpath.If this occures during eclipse build make sure you run eclipse under JDK as well ......  
구글링해보니 여러 해결방법이 보이는데 난 이클립스의 설정파일에 JVM경로를 명시해주는 것으로 해결했다.

이클립스 설치경로에 eclipse.ini 파일에 아래 2줄을 추가했다. 주의할 점은 -vmargs 설정 전에 해줘야한다.  

-g 옵션은 글로벌 패키지로 설치한다는 옵션으로 해당 PC 개발환경의 모든 프로젝트에서 사용이 가능하도록 하는 것이다.   

{% highlight bash %}
-vm
C:/Program Files/Java/jdk1.8.0_171/bin/javaw.exe
{% endhighlight %}

경로는 본인의 Java 설치 경로에 맞게 지정하면 되며 설정 후 이클립스를 다시 시작한 후 프로젝트에서 Maven > Update Project를 수행하니 오류가 없어지고 Q도메인이 인식됐다.
