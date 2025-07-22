# AWS Bedrock GenAI ETL Analysis Setup

This script sets up a complete AWS Bedrock GenAI environment for ETL analysis, including:

- OpenSearch Serverless collection and vector index
- Knowledge Base with S3 data source
- Bedrock Agent with ETL analysis capabilities
- Code Interpreter action groups

## Prerequisites

1. **AWS Credentials**: Ensure your AWS credentials are configured with appropriate permissions for:
   - OpenSearch Serverless
   - Amazon Bedrock
   - S3 access
   - IAM roles and policies

2. **IAM Roles**: The following IAM roles must exist in your account:
   - `BedrockKBRole` - Role for Bedrock Knowledge Base operations
   - `BedrockKnowledgeBaseAccessRole` - Additional access role for KB
   
3. **S3 Bucket**: An S3 bucket with your documents must be accessible:
   - Default bucket: `genai-test-dg`
   - Default prefix: `test-kb/`

## Installation

1. Clone or download the script files
2. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

## Configuration

Update the constants at the top of `kb_agent.py` if needed:

```python
REGION = "us-east-1"
COLLECTION_NAME = "test-genai-1"
S3_BUCKET_ARN = "arn:aws:s3:::genai-test-dg"
S3_PREFIX = "test-kb/"
ACCOUNT_ID = "406099943223"  # Update with your AWS account ID
```

## Usage

Run the complete setup:

```bash
python kb_agent.py
```

The script will:
1. Create OpenSearch Serverless security policies
2. Create and configure the vector collection
3. Set up the Knowledge Base with S3 data source
4. Start document ingestion
5. Create the Bedrock Agent with ETL analysis capabilities
6. Enable Code Interpreter and User Input action groups
7. Test the agent with a sample query

## ETL Analysis Capabilities

The agent is designed to analyze SQL stored procedures and extract column-level transformations. It can:

- Parse SQL stored procedures
- Identify source and target tables
- Map transformations between columns
- Classify transformation types (Direct Mapping, Expression, Lookup, No Transformation)
- Output results in structured JSON format

## Output

Upon successful completion, the script will display:
- Agent ID
- Alias ID  
- Knowledge Base ID

You can use these IDs to interact with the agent programmatically.

## Troubleshooting

1. **Permission Errors**: Ensure your AWS credentials have the necessary permissions
2. **Role Not Found**: Verify the IAM roles exist in your account
3. **S3 Access Issues**: Check bucket permissions and ensure the prefix exists
4. **Timeout Issues**: Some operations may take time; the script includes appropriate wait mechanisms

## Functions Overview

- `ensure_opensearch_policies()` - Creates security policies for OpenSearch
- `create_collection()` - Creates and configures the vector collection
- `create_knowledge_base()` - Sets up the Knowledge Base
- `create_agent()` - Creates the Bedrock Agent with ETL capabilities
- `invoke_agent()` - Tests the agent with queries

For more details, see the docstrings in the code.
