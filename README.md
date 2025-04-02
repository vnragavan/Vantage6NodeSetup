# Vantage6 Node Setup Guide

This guide outlines how to set up and run a vantage6 node against Cancer Registry of Norway's  Vantage6 server.

## Step 1: Requirements

Follow the node administration requirements from the official vantage6 documentation: [Vantage6 Node Requirements](https://docs.vantage6.ai/en/main/node/requirements.html)

Ensure you have installed:

- Python
- pip
- Docker and Docker Compose

## Step 2: Virtual Environment and Installation

Create a virtual environment and install vantage6:

```bash
python -m venv vantage6_env
source vantage6_env/bin/activate
pip install vantage6
```

## Step 3: Obtain an API Key and Sample Datasets
Send an email to ``Narasimha.Raghavan[at]kreftregisteret.no`` including your organization name and address to receive your API key and sample datasets (along with the datasets' label name) that you need as part of your node's configuration.

## Step 4: Register your node 
After receiving the API key and datasets, register your node against our server by running:
```bash
v6 node new
```

**You'll be prompted to enter the following details:**

- **Configuration name:** `<Name for your configuration>`
- **API:** `<API received from us>`
- **Base-URL of the server:** `https://fed-server.kreftregisteret.no`
- **Port:** `443`
- **Path of the API:** `/api`
- **Task directory path:** `/home/<username>/.local/share/vantage6/node/<configuration name>`
- **Add a database?:** `Y`
    - **Database label:** `<Label received from us>`
    - **DatabaseURI:** `<Path to the CSV file received from us>`
    - **Database type:** `csv`
- **Add another database?:** `n`
- **Connect to a VPN server?:** `N`
- **Limit algorithms allowed?:** `n`
- **Logging level:** `DEBUG`
- **Enable encryption?:** `n`

**[info]** - New configuration created:  
``/home/<username>/.config/vantage6/node/<configuration name>.yaml``  

**[info]** - You can start the node by running:  ``v6 node start``

## Step 4b: (2 nodes and synthetic datasets)
This step is needed only when there are 2 nodes in the consortium and both the nodes are using synthetic datasets. 
Add the following lines to your node's configuration file. The path can be located by checking the [info] message or by executing the command ``v6 node files``

```bash
algorithm_env:
  KAPLAN_MEIER_MINIMUM_ORGANIZATIONS: 2 
```
You can read more about the privacy guard of Vantage6 at the [Federated Kaplan Meier Official Vantage6 documentation](https://algorithms.vantage6.ai/en/latest/v6-kaplan-meier-py/docs/v6-kaplan-meier-py/privacy.html). 

## Step 5: Run your node 
To start your node, execute 
```bash
v6 node start
```

## Step 6: Documentation 
Further documentation can be found at the [official vantage6 documentation](https://docs.vantage6.ai/en/main/)_.
