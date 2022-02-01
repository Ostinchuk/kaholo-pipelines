# Synchronize Salesforce with MySQL

This pipeline synchronizes data between Salesforce object and a corresponding table in MySQL database.

## Requirements

1. Salesforce instance:
    - instance URL
    - Username
    - Password
    - Security token

2. MySQL database:
    - connection string ("server=127.0.0.1;port=3306;uid=root;pwd=12345;database=test")

3. Slack instance (optionally):
    - [incoming webhook URL](https://api.slack.com/messaging/webhooks)

## Vault items

The pipeline uses the following list of credentials (should be created in Vault):

- SALESFORCE_PASSWORD
- SALESFORCE_TOKEN
- SALESFORCE_USERNAME
- SALESFORCE_URL
- MYSQL_CONNECTION_STRING
- SLACK_INCOMING_WEBHOOK

## Pipeline configuration

You can find a default configuration object `SF_MySQL_config` in "Configurations" tab. You can adjust it to your needs.

Configuration settings:

1. `sf_object` - a Salesforce object to sync up.
2. `sf_limit` - the maximum number of Salesforce records to query in one request. This is a hard limit of Salesforce. You can make it smaller, but not bigger.
3. `database` - a database name.
4. `table_name` - a table for storing data from a corresponding Salesforce object.
5. `column_mapping` - an array of objects that map Salesforce fields and table columns  
    5.1 `sf_object_field` - a Salesforce object field. It is `null` if there is not a corresponding column in a table.  
    5.2 `column_name` - a name of a column in a table.  
    5.3 `data_type` - a data type and constraints.  

## How the pipeline works

The pipeline consists of six actions that use custom JavaScript functions and values from `SF_MySQL_config` object:

1. `CountRecords`: retrieves the total number of records for a given Salesforce object.
2. `SelectRecords`: based on the total number of records, iteratively queries the Salesforce object and constructs an array of records.
3. `DropTable`: drops a table if it exists. Every time the pipeline runs, a table recreates.
4. `CreateTable`: creates an empty table based on `column_mapping` array from the configuration object.
5. `InsertData`: inserts data into the table.
6. `Notify`: sends a Slack notification (`Inserted <NUMBER_OF_ROWS> rows into "<TABLE_NAME>" table.`).

## How to configure the pipeline

TODO
