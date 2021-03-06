# Your Infrastructure
By default, your DigitalOcean Droplets have some graphs and you have some idea of how your infrastructure is operating. You most likely have added other third party solutions or processes to further gather data about performance and availability. We're going to take a step back and cover Monitoring basics to help give you a fundamental structure to help build up your Monitoring practices.

There are a lot of concepts within Monitoring. There are books dedicated to these concepts and we will not have the opportunity to go into all the details. We'll break this section into the following concepts:
- Data Collection
 - Knowing what to collect
- Data Visualization
 - Overview of tools
 - Concepts for alerting
- Performance Testing

## Team Effort
Before we dig in, we want to touch on the subject of responsibility. Monitoring is not the responsibility of an individual or a team. Large organizations may have a team dedicated to Monitoring (Observability), but the goal of such a team would be to deliver the tools to allow development and ops teams the ability to monitor their own work. A developer will know the details of their application and what metrics are important. Everyone involved with your application and infrastructure has a vested interest in ensuring accurate and actionable monitoring is in place.

## Data Collection
Data. Your applications, services, and servers are generating an enormous amount of data. A whole lot of data. There are two easy paths to take that have nearly the same result. 1) Capture all data or 2) Capture barely any data. Either way, it will be hard to have actionable data to use in making decisions.  

Here are a few examples of actionable data:
- If you have an outage without an alert: You are missing a measurement or alert
- If you have alerts that do not correspond with an issue or an outage: You have an unnecessary alert 

The data will tell us when something is not right. However, if we wait for our data to tell us that, we've missed the boat. The data has a direct correlation with your business. We'll want to connect the dots between performance, reliability, and revenue. If downtime has a dramatic impact on your bottom line, then investing in added infrastructure as insurance is a good value. The metrics of your infrastructure go hand in hand with your revenue reports. 

Where do we start? It's hard to know where to begin knowing the importance of this data. We asked Brian Knox, the manager of the Observability team at DigitalOcean what he thought on the subject: "You need to focus on the important data and reduce the signal to noise ratio. Narrow down what is important and measure it in a way that clearly shows issues. If you start with two basic methods [RED and USE], you'll have the most important data and it'll be easier to interpret. It's easy to collect too much data, but it won't be usable."

We're going to start with two base methods for collecting and reviewing data:

## Monitoring Your Services  
Your application is made up of many services. Some may be custom applications, others may be simple deployments of Apache or MySQL. Many times these services rely on each other. The symbiotic nature of the services may lead to a perceived bottleneck in one service that is caused by a different service that the problematic service relies on. One of the most difficult issues I troubleshooted in my early sys-admin days was Apache overloading while MySQL looked perfectly fine, all while it was causing Apache to drive the server load to the point of a system crash.

### RED Method
#### [R]ate
*The number of requests per second the service is serving*
#### [E]rror Rate
*The number of failed requests per second*
#### [D]uration
*The time it takes for requests to be performed*

This data delivered by the RED Method[^1] will give you a clear picture of how well each service is running. It can be used to dial in the resources (servers) you need to dedicate to any given service. It's more important to use it as the metrics to be alerted by. Before creating alerts, you'll want to consider what each services tolerances are. How many reqeuests per second can be processed before customers start to see a problem, or what is an acceptable amount of errors. A spike in error rate or duration is a clear indicator your customers are seeing issues. 

Alerts triggered by an issue with a service may have many causes and it can be difficult to identify the cause. It is important to take closer looks in your performance monitoring and testing controls we'll discuss in the next chapters. 

## Monitoring Your Servers
Issues with services running slower or having errors may be caused by other services or a code deployment, but the cause may also be related to your servers as well. We recommend installing our opensource observability agent, do-agent[^3], on all Droplets. Within the DigitalOcean platform, we see all Droplet conditions from the perspective of the hypervisor. The do-agent software gives us more insight on what is happening inside of the Droplets. These insights are a good base-line and we'll want even more detail and clarity to expedite troubleshooting. 

There is a method we can apply to monitoring server resources that will give vital data when troubleshooting more difficult issues.

### USE Method
#### [U]tilization
*Average use of a resoruce*
#### [S]aturation 
*The amount of available or overusage of a resource*
#### [E]rrors
*Error counts*

The USE method[^2] can be applied to the three main aspects of performance monitoring and tuning:
- CPU
- I/O
- Network 

Looking at CPU utilization including all of the CPU measurement statistics, as well as system load averages, will give a clear indicator of system health. I/O includes memory and storage usage, but also would include speed related aspects. I/O Operations per Second (IOPS) would be the measurement of the storage performance. Network would similarly have bandwidth utilization as a metric, but also can generate error counts that would be indicative of possible network hardware or physical network connection issues.


In the next chapter we'll apply these monitoring methods to your infracture with tools and visualisations. The importance of this chapter was to highlight ways to be mindful of the data you intend to collect. Too much data or not the right data will not give you a clear picture of your infrastructure and will lead to uninformed decisions. 



--- 
*These methods are only summarized here. If you want to dive deeper in the world of monitoring we suggest you look at other resources like the Google SRE book[^4], or attend a conference like Monitorama[^5].*


[^1]: RED Method https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/
[^2]: USE Method http://www.brendangregg.com/usemethod.html
[^3]: do-agent https://blog.digitalocean.com/improved-graphs/
[^4]: Google SRE Book https://landing.google.com/sre/book/chapters/monitoring-distributed-systems.html
[^5]: Monitorama Conference http://monitorama.com/ 








