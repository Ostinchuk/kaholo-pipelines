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
    - incoming webhook URL

## Pipeline configuration

You can find a default configuration object `SF_MySQL_config` in "Configurations" tab. You should adjust it to your needs.

Configuration settings:

1. `sf_object` - a Salesforce object to sync up.
2. `sf_limit` - the maximum number of Salesforce records to query in one request. This is a hard limit of Salesforce. You can make it smaller, but not bigger.
3. `database` - a database name.
4. `table_name` - a table for storing data from a corresponding Salesforce object.
5. `column_mapping` - an array of objects that map Salesforce fields and table columns  
    5.1 `sf_object_field` -   
    5.2 `column_name` -   
    5.3 `data_type` -   
