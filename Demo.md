# Step 1
You should already finish this prompts https://github.com/ISG-ICS/CS230/blob/main/hadoop_on_aws_ec2.md
# Stap 2 
- On Master node only: Run the following command in `<HadoopInstallationFolder>/sbin/` folder to start your cluster. It will take a while.
```
./start-dfs.sh
./start-yarn.sh
```
- Set `<HadoopInstallationFolder>/etc/hadoop/hadoop-env.sh`
```bash
export PATH=${JAVA_HOME}/bin:${PATH}
export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
```
- Create the dictionary
```
./hadoop fs -mkdir -p /user/terry/wordcount/input/
#/user/terry/wordcount/input/   terry is my name , you can write anything you want
```
- Write the example.txt(Dear Bear River Car Car River Deer Car Bear)
```
nano example.txt
```
- Save and exit
```
'ctrl+x' then presss 'y' then press 'return'
```

- Put example.txt into the dictionary under HDFS
```
./hadoop fs -put example.txt /user/terry/wordcount/input
```
- Check if example.txt successfully put into the place we set
```
./hadoop fs -ls /user/terry/wordcount/input/
```
If success, you should see this:

![txt](https://github.com/Terrylin2023/wordcountCS230/blob/main/text.png)

- Then, check the content
```
./hadoop fs -cat /user/terry/wordcount/input/example.txt
```
Dear Bear River Car Car River Deer Car Bear


- Edit the file
  (https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html)
  Copy the code from WordCount v2.0
```
nano WordCount2.java
```
- Save and exit
```
'ctrl+x' then presss 'y' then press 'return'
```
- Compile WordCount2.java and create a jar
```
./hadoop com.sun.tools.javac.Main WordCount2.java
jar cf wc.jar WordCount*.class
```

- Run the application
```
./hadoop jar wc.jar WordCount2 /user/terry/wordcount/input /user/terry/wordcount/output
```

- Output(the file part-r-00000 should be generated automatically)
```
./hadoop fs -cat /user/terry/wordcount/output/part-r-00000
```
## Finally,
![Result](https://github.com/Terrylin2023/wordcountCS230/blob/main/Result.png)

Ref(https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html)
