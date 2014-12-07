webcrawler
==========

Prerequisities:
Apache Nutch 1.9 - http://tux.rainside.sk/apache/nutch/1.9/apache-nutch-1.9-bin.zip <br />
Apache Solr 4.10.2 - http://tux.rainside.sk/apache/lucene/solr/4.10.2/solr-4.10.2.zip <br />
Oracle JAVA 8 - http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html <br />
Configuration files - https://github.com/jkmetko/webcrawler/configuration_files <br />

<strong>!Note</strong> - for useage on Windows, install: <br />
Cygwin - https://cygwin.com/install.html

____________________

<h1>Setup:</h1>
1) Install Oracle JAVA 8

2) Setup new environment variable JAVA_HOME environment variable -  http://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/index.html

3) Export all the nutch and solr files to new folder called crawlerHome, we'll refered to this folder as {home}, to crawlerHome/solr4.10.2 as {SOLR_home}, and to ho crawlerHome/nutch-1.9 as {NUTCH_home}.
Copy files from "Configuration files" to {home}/configuration_files . We'll refer to it as {conf}

4) Open {NUTCH_home}/conf/nutch-site.xml and add the agent name value
Example:
<property>
 <name>http.agent.name</name>
 <value>My Nutch Spider</value>
</property>

5) Create a URL seedlist - open {NUTCH_home/bin/} and create new folder "urls". In this folder, add file "seeds.txt" and put in sites you want to crawl, eg. http://www.economist.com

6) Create REGEX internal constrains
copy files from {confs}/regex-urlfilter.txt to {NUTCH_home}/conf
Change domain/s to that/those in seeds.txt

<strong>!NOTE</strong> - some file extensions are deprecated. Feel free to change them.

7) Copy files from {conf}/Nutch to {NUTCH_home}/conf/schema.xml

8) Copy file from {conf}/Solr/ to {SOLR_home}/example/solr/collection1/conf/

9) Start Apache Solr from terminal:
  - cd {SOLR_home}/example
  - java -jar start.jar

<strong>!NOTE</strong> verify service start up. In browser type in url "http://localhost:8983/solr"

10) Start your first crawl:
  - cd {NUTCH_home}/bin
  - ./crawl urls/ economistCrawl/ http://localhost:8983/solr/collection1 2

<strong>!NOTE</strong> - for description of this service, run "./crawl"

11) Make your first search query in SOLR:
  - visit http://localhost:8983/solr/collection1/browse
  - type in your query
  - see results


