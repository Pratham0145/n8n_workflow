1. Install MCP Toolbox
Download the latest version of Toolbox as a binary:
```
# for win os

curl -O https://storage.googleapis.com/genai-toolbox/v0.13.0/windows/amd64/toolbox.exe
```

2. Configure MySQL Connection
Create a tools.yaml file with your MySQL configuration. Here's an example adapted for MySQL:

```
sources:
  my-mysql-source:
    kind: mysql
    host: 
    port: 
    database: 
    user: 
    password: 

tools:
  # Tool to get database schema information
  get-table-schema:
    kind: mysql-sql
    source: my-mysql-source
    description: Get the schema information for all tables in the database including table names, column names, data types, and constraints.
    parameters: []
    statement: |
      SELECT 
        TABLE_NAME,
        COLUMN_NAME,
        DATA_TYPE,
        IS_NULLABLE,
        COLUMN_DEFAULT,
        COLUMN_KEY,
        EXTRA,
        COLUMN_COMMENT
      FROM INFORMATION_SCHEMA.COLUMNS 
      WHERE TABLE_SCHEMA = DATABASE()
      ORDER BY TABLE_NAME, ORDINAL_POSITION;

  # Tool to get specific table schema
  get-specific-table-schema:
    kind: mysql-sql
    source: my-mysql-source
    description: Get detailed schema information for a specific table.
    parameters:
      - name: table_name
        type: string
        description: The name of the table to get schema for.
    statement: |
      SELECT 
        COLUMN_NAME,
        DATA_TYPE,
        IS_NULLABLE,
        COLUMN_DEFAULT,
        COLUMN_KEY,
        EXTRA,
        COLUMN_COMMENT
      FROM INFORMATION_SCHEMA.COLUMNS 
      WHERE TABLE_SCHEMA = DATABASE() AND TABLE_NAME = ?
      ORDER BY ORDINAL_POSITION;

  # Tool to list all tables
  list-tables:
    kind: mysql-sql
    source: my-mysql-source
    description: List all tables in the current database.
    parameters: []
    statement: |
      SELECT 
        TABLE_NAME,
        TABLE_TYPE,
        TABLE_COMMENT
      FROM INFORMATION_SCHEMA.TABLES 
      WHERE TABLE_SCHEMA = DATABASE();

  # Tool for dynamic SQL execution - NO PARAMETERS for mysql-execute-sql
  execute-sql-query:
    kind: mysql-execute-sql
    source: my-mysql-source
    description: Execute a custom SQL query. Use this tool to run SELECT, INSERT, UPDATE, or DELETE statements. The agent will provide the full SQL query.

toolsets:
  dynamic-mysql-toolset:
    - get-table-schema
    - get-specific-table-schema
    - list-tables
    - execute-sql-query
```

### **NOTE : TOOLBOX.exe and TOOLS.yaml file should be in same location**


3. Start the Toolbox Server
Run the Toolbox server:

```
./toolbox --tools-file "tools.yaml"

```


Toolbox supports HTTP transport protocol Connect via MCP Client | MCP Toolbox for Databases and will be available at 
```
http://127.0.0.1:5000/mcp.
```

Testing Your Setup
Use MCP Inspector for testing and debugging Toolbox server Quickstart (MCP) | MCP Toolbox for Databases before integrating with n8n:

```
npx @modelcontextprotocol/inspector
```


Configure it to connect to http://127.0.0.1:5000/mcp with "Streamable HTTP" transport type.
This setup allows your n8n workflows to interact with MySQL databases through the MCP Toolbox, providing a secure and efficient way to perform database operations within your AI agent workflows.

