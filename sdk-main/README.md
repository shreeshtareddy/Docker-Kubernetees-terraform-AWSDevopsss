# sdk




---

### 📄 `README.md`

```markdown
# AWS S3 Bucket Creation with Boto3 in VS Code

This project shows how to create an AWS S3 bucket using the AWS SDK for Python (Boto3). It was developed and executed in **VS Code**.

---

## 🛠️ Tools Used

- **Python 3.x**
- **Visual Studio Code (VS Code)**
- **AWS SDK for Python (Boto3)**
- **AWS CLI**

---

## 📁 Project Files

- `code.py` — Python script to create an S3 bucket.
- `results.txt` — Contains the sample output:  
  ```
  Hello from AWS SDK!
  ```

---

## ✅ Steps to Run This Project

### 1. Open VS Code

Create a folder for your project and open it in VS Code.

### 2. Create Your Python Script

Create a file named `code.py` and paste this code:

```python
import boto3
from botocore.exceptions import ClientError

# Replace with your region
region = 'us-east-1'  # or 'ap-south-1', 'us-west-2', etc.
bucket_name = 'bucket174463276'  # Make sure this is unique globally

# Initialize session
session = boto3.session.Session(region_name=region)
s3 = session.client('s3')

try:
    if region == 'us-east-1':
        s3.create_bucket(Bucket=bucket_name)
    else:
        s3.create_bucket(
            Bucket=bucket_name,
            CreateBucketConfiguration={'LocationConstraint': region}
        )
    print(f'Bucket "{bucket_name}" created successfully in {region}')
except ClientError as e:
    if e.response['Error']['Code'] == 'BucketAlreadyOwnedByYou':
        print(f' Bucket "{bucket_name}" already exists and is owned by you.')
    else:
        print(f' Failed to create bucket: {e}')
```

![Screenshot 2025-04-15 113100](https://github.com/user-attachments/assets/ace1871d-d04d-4dfa-b42d-db8fa160348b)

### 3. Set Up AWS CLI (One Time)

If you haven’t configured AWS CLI yet:

```bash
aws configure
```

You’ll be prompted to enter:
- AWS Access Key ID
- AWS Secret Access Key
- Default region (e.g. `us-east-1`)
- Default output format (press enter for default)

### 4. Install Boto3

In the terminal inside VS Code, run:

```bash
pip install boto3
```

### 5. Run the Script

Run your script using:

```bash
python code.py
```

If everything is set up correctly, you should see:

```
Bucket "bucket174463276" created successfully in us-east-1
```

Or a message if the bucket already exists.

---
![Screenshot 2025-04-15 113115](https://github.com/user-attachments/assets/83eaec40-3be9-43de-a074-5ab31bc28311)
