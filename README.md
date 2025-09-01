# n8n Workflow – Fetch Data using MCP

This repository contains an **n8n workflow** that demonstrates how to fetch data from **MySQL** using **MCP (Model Context Protocol)**.

## 📂 Folder Structure

n8n_workflow/
└── Fetch-data using MCP/
└── MYSQL using MCP.json


- **`MYSQL using MCP.json`** → The n8n workflow file that can be imported into your n8n instance.

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Pratham0145/n8n_workflow.git
cd n8n_workflow
```

2. Open n8n

Start your n8n instance locally or on server:

```bash
n8n start
```

3. Import the Workflow

Open the n8n UI in your browser (default: http://localhost:5678).

Go to Workflows → Import from File.

Select the file:

Fetch-data using MCP/MYSQL using MCP.json


Save the workflow.

⚙️ Configuration

Before running the workflow, configure:

MySQL Credentials

Go to Credentials → New → MySQL

Enter:

Host

Port (default: 3306)

Database name

Username

Password

MCP Settings

Make sure your MCP server is running and accessible.

Update MCP connection details inside the workflow nodes if needed.

▶️ Running the Workflow

Open the workflow in n8n.

Click Execute Workflow.

The workflow will:

Connect to MySQL using MCP

Fetch the data

Output results in n8n

📖 Notes

This workflow is designed for testing MCP integration with MySQL in n8n.

You can extend it by adding more nodes for transformations, filtering, or connecting to other services.

📝 License

This project is licensed under the MIT License.


---

Would you like me to also **add a "Preview" section with a sample screenshot placeholder** 
