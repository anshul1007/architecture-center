---
title: Time series data
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Time series solutions

Time series data is a set of values organized by time. Examples of time series data include sensor data, stock prices, click stream data, and application telemetry. Time series data can be analyzed for historical trends, real-time alerts, or predictive modeling.

![Time Series Insights](./images/time-series-insights.png) 

Time series data represents how an asset or process changes over time. It’s unique in that it has a timestamp and time is most meaningful as an axis. Time series data typically arrives in order of time and is usually treated as an insert rather than an update to your database. Because of this, change is measured over time, enabling you to look backward and to predict future change. As such, time series data is best visualized with scatter or line charts.

![Time series data visualized in a line chart](./images/time-series-chart.png)

Some examples of time series data are:

- Stock prices captured over time to detect trends, review past performance, and even conduct some level of prediction.
- Server performance, such as CPU usage, IO load, memory usage, and network bandwidth consumption.
- Telemetry captured from temperature sensors on industrial equipment, providing real-time, valuable data on temperature readings that can be used to detect pending equipment failure and trigger alert notifications.
- Combine incoming real-time car telemetry data including speed, braking, and acceleration over a time window to produce an aggregate risk score for the driver.

In each of these cases, you can see how time is most meaningful as an axis. Displaying the events in the order in which they arrived is a key characteristic of time series data, as there is a natural temporal ordering. This differs from data captured for standard OLTP data pipelines where data can be entered in any order, and updated at any time.

## When to use this solution

Choose a time series solution when you need to ingest data whose strategic value is centered around changes over a period of time, and you are primarily inserting new data and rarely updating, if at all. You can use this information to detect anomalies, visualize trends, compare current data to historical data, among other things. This type of architecture is also best suited for predictive modeling and forecasting results, because you have historical record of changes over time that can then be applied to any number of forecasting models. Forecasting means understanding how a metric moves through time and being able to project/predict the future.

Using time series offers the following benefits:

* Clearly represents how an asset or process changes over time.
* Helps you quickly detect changes to a number of related sources, making anomalies and emerging trends clearly stand out.
* Best suited for predictive modeling and forecasting.

### Internet of Things (IoT)

Data collected by IoT devices is a natural fit for time series storage and analysis. The incoming data is inserted and rarely, if ever, updated. The data is time stamped and inserted in the order it was received, and this data is typically displayed in chronological order, enabling users to discover trends, spot anomalies, and use the information for predictive analysis.

For more information, see [Internet of Things](../concepts/big-data.md#internet-of-things-iot).

### Real-time analytics

Often, data is most valuable at its time of arrival. Whether your data is streaming into your real-time pipeline from connected IoT devices, or from telemetry originating from security monitoring software, there is a growing need for deriving insights from the millions of events being generated in real time. Any delay in insights can cause significant downtime and business impact. Additionally, the need to correlate data from a variety of different sources, such as sensors, is paramount to debug and optimize business processes and workflows. Reducing the time and expertise required for this is essential for businesses to gain a competitive edge and optimize their operations.

Ideally, you would have a stream processing layer that can handle the influx of data and process all of it with high precision and high granularity. This isn't always possible, depending on your streaming architecture and the components of your stream buffering and stream processing layers. You may need to sacrifice some precision of the time series data by reducing it. This is done by processing sliding windows of several seconds apiece, allowing the processing layer to perform calculations in a timely manner. If you are capable of capturing full fidelity of your streaming data, you need the compute power and ability to down sample (through aggregates) your data when displaying longer periods of time, such as zooming out your graph to display data captured over several months, for example.

## Challenges

Establishing a time series architecture can have some of the following challenges:

* Time series data is often very high volume, especially in IoT scenarios. Storing, indexing, querying, analyzing, and visualizing time series data can be challenging. 
* Finding the right combination of high-speed storage and powerful compute operations for handling real-time/near real-time analytics, while minimizing time to market and overall cost investment.

## Architecture

In many scenarios that involve time series data, such as IoT, the data is captured in real time. As such, as [real-time processing](./real-time-processing.md) architecture is appropriate. 

Data from one or more data sources is ingested into the stream buffering layer by a [IoT Hub](/azure/iot-hub/), [Event Hubs](/azure/event-hubs/), or [Kafka on HDInsight](/azure/hdinsight/kafka/apache-kafka-introduction). Next, the data is processed in the stream processing layer that can optionally hand off the processed data to a machine learning service for predictive analytics. The processed data is stored in an analytical data store, such as [HBase](/azure/hdinsight/hbase/apache-hbase-overview), [Azure Cosmos DB](/azure/cosmos-db/), Azure Data Lake, or Blob Storage. An analytics and reporting application or service, like Power BI or OpenTSDB (if stored in HBase) can be used to display the time series data for analysis.

Another option is to use [Azure Time Series Insights](/azure/time-series-insights/). Time Series Insights is a fully managed service for time series data. In this architecture, Time Series Insights performs the roles of stream processing, data store, and analytics and reporting. It accepts streaming data from either IoT Hub or Event Hubs and stores, processes, analyzes, and displays the data in near real time (1 minute intervals). It does not pre-aggregate the data, but stores the raw events.

Time Series Insights is schema adaptive, which means that you do not have to do any data preparation to start deriving insights. This enables you to explore, compare, and correlate a variety of sensors seamlessly. It also provides SQL-like filters and aggregates, ability to construct, visualize, compare, and overlay various time series patterns, heat maps, and the ability to save and share queries. 

## Technology choices

- [Data Storage](../technology-choices/data-storage.md)
- [Analysis, visualizations, and reporting](../technology-choices/analysis-visualizations-reporting.md)
- [Analytical Data Stores](../technology-choices/analytical-data-stores.md)
- [Stream processing](../technology-choices/stream-processing.md)