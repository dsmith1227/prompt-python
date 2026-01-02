# Prompt Python - AI-Powered Data Analysis with S3 Integration

An AI-powered data analysis application that reads CSV files from AWS S3 and provides natural language analysis using Google Gemini AI.

## Features

- **S3 Integration**: Load CSV files directly from AWS S3 buckets
- **Conversational AI**: Ask questions about your data in natural language
- **Automated Visualizations**: Generate professional charts and graphs automatically
- **Statistical Analysis**: Get insights, correlations, and statistical summaries
- **Chat Interface**: Persistent conversation history for iterative analysis

## Prerequisites

1. **Python 3.8+**
2. **Google API Key**: Get one from [Google AI Studio](https://makersuite.google.com/app/apikey)
3. **AWS Account**: With S3 access and appropriate credentials
4. **AWS IAM Permissions**: User must have `s3:GetObject` permission for the target bucket

## Installation

1. Clone the repository and navigate to the project directory

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Configure environment variables in `.env` file:
```bash
# Google AI API Key
GOOGLE_API_KEY=your_google_api_key_here

# AWS Credentials for S3 Access
AWS_ACCESS_KEY_ID=your_aws_access_key_id_here
AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key_here
AWS_REGION=us-east-1
```

## Usage

1. Start the application:
```bash
streamlit run app.py
```

2. Configure in the sidebar:
   - **Google API Key**: Enter your Google AI API key (or set in `.env`)
   - **AWS Credentials**: Enter AWS Access Key ID and Secret Access Key (or set in `.env`)
   - **AWS Region**: Specify your S3 bucket region (default: us-east-1)

3. Load data from S3:
   - **S3 Bucket Name**: Enter the name of your S3 bucket (e.g., `my-data-bucket`)
   - **S3 Object Key**: Enter the full path to your CSV file (e.g., `data/sales-2024.csv`)
   - Click **"Load Data from S3"**

4. Start analyzing:
   - Once data is loaded, ask questions in natural language
   - Examples:
     - "What are the summary statistics?"
     - "Show me a correlation matrix"
     - "Visualize the distribution of sales by region"
     - "What are the top 10 products by revenue?"

## AWS S3 Setup

### Creating an IAM User for S3 Access

1. Go to AWS IAM Console
2. Create a new user or use an existing one
3. Attach a policy with at least `s3:GetObject` permission:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

4. Generate access keys and save them securely

### S3 Bucket Configuration

- Ensure your CSV files are in a readable format
- The bucket should allow access from your IAM user
- For cross-account access, configure appropriate bucket policies

## Configuration Options

### Environment Variables

You can configure credentials in two ways:

1. **Via `.env` file** (recommended for local development):
```bash
GOOGLE_API_KEY=your_key_here
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
```

2. **Via Streamlit interface**: Enter credentials directly in the sidebar

## Security Notes

- Never commit your `.env` file with real credentials to version control
- Use IAM roles with minimum required permissions
- Consider using AWS Secrets Manager or Parameter Store for production deployments
- Rotate AWS access keys regularly
- For production, consider using AWS STS temporary credentials

## Error Handling

The application provides detailed error messages for common issues:

- **Invalid Credentials**: Check your AWS access keys
- **Bucket Not Found**: Verify the bucket name is correct
- **Access Denied**: Ensure your IAM user has the required permissions
- **Object Not Found**: Check that the S3 key path is correct
- **Invalid CSV**: Ensure the file is properly formatted

## Architecture

- **Frontend**: Streamlit
- **AI Engine**: Google Gemini (via LangChain)
- **Data Processing**: Pandas, NumPy
- **Visualizations**: Matplotlib, Seaborn, Plotly
- **Cloud Storage**: AWS S3 (via boto3)

## Limitations

- Only supports CSV files
- Maximum file size depends on available memory
- Analysis quality depends on data quality and structure
- Requires active internet connection for AI processing

## Troubleshooting

**Issue**: "AWS credentials not found"
- **Solution**: Ensure AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY are set

**Issue**: "Access denied" when loading from S3
- **Solution**: Check IAM permissions include `s3:GetObject` for the bucket

**Issue**: "Bucket does not exist"
- **Solution**: Verify bucket name and ensure it's in the specified region

**Issue**: Google API key error
- **Solution**: Generate a new key from Google AI Studio

## License

See LICENSE file for details.
