# IPAT Framework 
Intigaration Performnace Analysis Tools
To collect Metrics, Traces , Logs By Using Open Source Demo Applicatipons and tools

What are the performance analysis tools?
Performance analysis tools support the application developer in 
tuning the application's performance for a given architecture. 
They measure performance data during the execution of the application and
provide means to analyze and interpret the provided data and to detect
performance bottlenecks.

opentelemetry
 
 PreRequeries:--
 1.Vscode
 2.sample application source code file/jar file
 3.Opentelemetry Javaagent -jarFilec
 4.prtometheus.exe
 5.zipkin.exe
 6.promtail.exe
 7.loki.exe
 8.grafana 9.2.6.exe

1.open source code of sample application in vscode ide and convert into jar file.

2.Auto instrumentation
 -- Frist Download opentelemetry javaagent jarfile
 -- To do instrumentation we create run.sh file 
 -- and write instumentaion code like we can see below 
 -- java -javaagent:(path for opentelmetry javaagent jar file) -jar (path of sample application.jar file) 

3.Export metrics to promotheus
 --Frist download prometheus local-sever file
 -- goto .yaml file and add code for export the traces 
 -- below see code 

 - job_name: "PETCLINIC"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9464"]
 -- run the prometheus at localy (prometheus.exe file)
 -- And also add code in vscode at run.sh file  to export traces prometheus like below see code

     -Dotel.metrics.exporter=prometheus \
     -Dotel.exporter.prometheus.port=9464 \
     -Dotel.exporter.prometheus.host=127.0.0.1 \
-- Finally save it all and run the run.sh file 
-- Now view the metrics in the prometheus.
--goto browser type localhost:9090 to see the traces in Zipkin

  Link:http://localhost:9090


4.Export traces to zipkin

--Frist download zipkin local-sever file
--Run Zipkin server locally in cmd 
  
  java -jar zipkin-server.jar

--Add export code in vscode at run.sh below we can see 

    -Dotel.traces.exporter=zipkin \

--Finally saveit and run the file

--goto browser type localhost:9411 to see the traces in Zipkin

     Link:http://localhost:9411

5.Traces and metrics Visulization in grafana

--Download the grafana-server file 
--goto bin folder run the .exe file
--now grafana server will running localy
--got browser enter the link http://localhost:3000

--for metrics 

--add data sources prometheus agent in grafana
-- enter quieries and run quiere

--for traces

--add data sources zipkin(1598) agent in grafana
-- enter trace id and run quiere

6.Export logs to loki

--first download the promtail and loki set-up files 
--add config files 

https://github.com/grafana/loki


OpenTeletry resolves one big pain: creating a standard to report and transmit measurements.
If you use OpenTelemetry with solution A, you can easily change your observability platform to solution B. Without losing any history of your traces.