import boto3
import json

# AWS Glue Configuration
CRAWLER_NAME = "athena fire_data schedule"  # Replace with your Glue Crawler name

# Initialize Glue client
glue_client = boto3.client("glue")

def lambda_handler(event, context):
    try:
        # Log the S3 event
        print("S3 Event Received:", json.dumps(event, indent=2))

        # Iterate through each S3 event record
        for record in event['Records']:
            bucket_name = record['s3']['bucket']['name']
            object_key = record['s3']['object']['key']
            print(f"File uploaded: s3://{bucket_name}/{object_key}")

            # Ensure the folder prefix matches
            if bucket_name == "lafiredata" and object_key.startswith("scraped_fire_data/"):
                print(f"Triggering Glue Crawler: {CRAWLER_NAME}")
                glue_response = glue_client.start_crawler(Name=CRAWLER_NAME)
                print(f"Glue Crawler triggered successfully: {glue_response}")
            else:
                print("File not in the expected folder. Skipping.")

        return {
            "statusCode": 200,
            "body": json.dumps("Glue Crawler triggered successfully.")
        }
    except Exception as e:
        print(f"Error triggering Glue Crawler: {str(e)}")
        return {
            "statusCode": 500,
            "body": json.dumps(f"Error: {str(e)}")
        }
