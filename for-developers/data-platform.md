---
description: >-
  Learn about the services Synthetix uses to collect, store, aggregate, and
  visualize data related to activity on Synthetix V3.
---

# Data Platform

### Intro

The Synthetix [Data Stack](https://github.com/Synthetixio/data) repository contains a collection of services that collect raw data, clean and aggregate that data, and create helpful visualizations to understand activity on Synthetix V3. You can visit a hosted instance of the resulting [Streamlit dashboard](https://synthetix.streamlit.app/).

### The Services

A number of services are required to create a complete view of the historical data and produce these dashboards. The linked github repo contains the technical documentation for standing the services up to run an instance of this database and dashboard yourself. The services are:

* A postgres database
* One subsquid indexer for each chain
* Scripts for collecting data using RPC calls
* Dbt models for data cleaning, transformation, and aggregation
* A streamlit dashboard for visualization

### Running an Instance

These services are relatively lightweight and do not require massive amounts of storage. It is possible to run the entire service locally on most modern consumer hardware, given you have access to archive RPC nodes for each blockchain.

The repo has a Docker compose file detailing these services and their configurations. Users can choose to comment out certain services.

For more details or to ask more questions about running an instance, you can ask in the #dev-portal channel in the Synthetix discord.
