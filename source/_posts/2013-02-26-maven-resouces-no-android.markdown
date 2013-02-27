---
layout: post
title: "Maven resouces no Android"
date: 2013-02-26 22:23
comments: true
categories: 
- maven
- android
---

Como muitos sabem é possivel criar projetos para android usando o [maven] [1]. Mais quando precisei utilizar o plugin [resources] [2] nava funcionou.

Depois de muita pesquisa no google, nada funcionava ainda rsrs. Então conversando com o brother [Nycholas] [3] que ja havia passado pelo mesmo problema consegui resolver. :)

Como h&aacute; pouco conteudo vou documentar aqui.

O maven resources por padr&atilde;o considera somente os diret&oacute;rios _src/main/resources_ e _src/test/resources_ e quando compiliado o projeto os arquivos ficam no diretorio _classes_. Para mudar isso precisamos adicionar as seguintes linhas ao _pom.xml_:

{% codeblock pom.xml %}
<build>
  <resources>
		<resource>
			<directory>${project.basedir}/res</directory>
			<filtering>true</filtering>
			<targetPath>${project.build.directory}/filtered-res</targetPath>
			<includes>
				<include>**/*</include>
			</includes>
		</resource>
		<resource>
			<directory>${project.basedir}/res</directory>
			<filtering>false</filtering>
			<targetPath>${project.build.directory}/filtered-res</targetPath>
			<excludes>
				<exclude>**/*</exclude>
			</excludes>
		</resource>
	</resources>
</build>
{% endcodeblock %}

Onde _directory_ &eacute; o diret&oacute;rio onde estão os seus resources e _targetPath_ &eacute; o diret&oacute;rio onde vai ser gerado os novos resources antes de empacotar no apk.

Agora &eacute; s&oacute; brincar. Espero ter ajudado.

[1]: http://code.google.com/p/maven-android-plugin/wiki/GettingStarted "Maven Android Plugin"
[2]: http://maven.apache.org/plugins/maven-resources-plugin/ "Maven Resouces Plugin"
[3]: https://twitter.com/o_lalertom