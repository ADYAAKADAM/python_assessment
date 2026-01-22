# S3 File Manager

A web-based file management application built with Django that provides a user-friendly interface for managing Amazon S3 buckets and files.

## Features

### 📁 Bucket Management
- List all S3 buckets in your AWS account
- Create new S3 buckets with proper region configuration
- Delete existing buckets (with all contents)
- Select and navigate between different buckets

### 📂 Folder Operations
- Create folders within S3 buckets
- Delete folders and all their contents
- Navigate through folder hierarchies with breadcrumb navigation
- View folder structure and contents

### 📄 File Management
- Upload files to S3 buckets and folders
- Download files directly from the interface
- Delete individual files
- Copy files within the same bucket
- Move files between locations in S3

### 🌐 User Interface
- Clean, responsive Bootstrap-based interface
- Real-time feedback with success/error messages
- Intuitive navigation with breadcrumb trails
- Mobile-friendly design

## Prerequisites

- Python 3.8 or higher
- AWS account with S3 access
- Virtual environment (recommended)

## Installation

### 1. Clone and Setup

```bash
# Navigate to your project directory
cd /path

# Create virtual environment
python3 -m venv 

# Activate virtual environment
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. AWS Configuration

Create a `.env` file in the project root with your AWS credentials:

```env
AWS_ACCESS_KEY_ID=your_access_key_id
AWS_SECRET_ACCESS_KEY=your_secret_access_key
AWS_STORAGE_BUCKET_NAME=your-default-bucket-name
AWS_S3_REGION_NAME=your-region-name  # e.g., us-east-1, eu-west-1, etc.
```

### 3. Django Setup

```bash
# Run migrations
python manage.py migrate

# Create superuser (optional, for admin access)
python manage.py createsuperuser

# Start development server
python manage.py runserver
```

The application will be available at `http://localhost:8000`

## Usage

### Accessing the Application

1. Open your web browser and navigate to `http://localhost:8000`
2. The main interface will display your S3 buckets and file management options

### Managing Buckets

#### Viewing Buckets
- All available buckets will be listed in the dropdown menu
- Select any bucket to view its contents

#### Creating a New Bucket
1. Enter a unique bucket name in the "New Bucket Name" field
2. Click "Create Bucket"
3. The new bucket will appear in the bucket list

#### Deleting a Bucket
1. Select the bucket you want to delete
2. Click the "Delete Selected Bucket" button
3. Confirm the deletion (this will remove ALL contents)

### Managing Folders

#### Creating Folders
1. Select a bucket or navigate to a folder
2. Enter the folder name in "New Folder Name" field
3. Click "Create Folder"

#### Deleting Folders
1. Navigate to the folder you want to delete
2. Click the "Delete" button next to the folder
3. Confirm deletion (removes folder and ALL contents)

### Managing Files

#### Uploading Files
1. Select a bucket or folder
2. Choose a file using the file selector
3. Click "Upload File"

#### Downloading Files
- Click the "Download" button next to any file

#### Deleting Files
1. Click the "Delete" button next to any file
2. Confirm the deletion

#### Copy/Move Files
1. Click "Copy/Move" button next to a file
2. Specify the destination path
3. Choose "Copy" or "Move" action
4. Click "Perform Action"

## Project Structure

```
s3_file_manager/
├── s3_project/          # Main Django project
│   ├── settings.py      # Project settings and AWS configuration
│   ├── urls.py          # URL routing
│   └── wsgi.py          # WSGI deployment
├── s3files/             # Main application
│   ├── views.py         # Business logic and S3 operations
│   ├── models.py        # Data models
│   ├── urls.py          # App URL patterns
│   └── migrations/      # Database migrations
├── templates/           # HTML templates
│   └── s3files/
│       └── index.html   # Main interface template
├── static/              # Static files (CSS, JS)
├── media/               # Uploaded media files
├── .env                 # Environment variables (not in version control)
├── requirements.txt     # Python dependencies
└── manage.py           # Django management script
```

## AWS Permissions Required

Your AWS credentials need the following S3 permissions:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:ListBucket",
                "s3:GetBucketLocation",
                "s3:CreateBucket",
                "s3:DeleteBucket",
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:CopyObject"
            ],
            "Resource": "*"
        }
    ]
}
```

## Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `AWS_ACCESS_KEY_ID` | AWS Access Key ID | Yes | - |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Access Key | Yes | - |
| `AWS_STORAGE_BUCKET_NAME` | Default bucket name | No | - |
| `AWS_S3_REGION_NAME` | AWS region | No | `us-east-1` |

## Troubleshooting

### Common Issues

**1. "IllegalLocationConstraintException"**
- Ensure your region is correctly specified in the `.env` file
- For regions other than `us-east-1`, the `LocationConstraint` is required

**2. "NoCredentialsError"**
- Verify your AWS credentials in the `.env` file
- Ensure the `.env` file is in the project root directory

**3. Redirect Errors**
- Make sure all redirect URLs include the proper path prefix (`/?`)

**4. Template Not Found**
- Verify the `templates` directory is correctly configured in `settings.py`
- Check that template files exist in the correct location

### Debugging

Enable Django debug mode by setting `DEBUG = True` in `settings.py` for detailed error messages during development.

## Security Considerations

⚠️ **Important Security Notes:**

1. **Never commit credentials**: Keep your `.env` file out of version control
2. **Use IAM roles**: In production, use IAM roles instead of hardcoded credentials
3. **HTTPS**: Always use HTTPS in production environments
4. **Access control**: Implement proper user authentication for multi-user scenarios
5. **CSRF protection**: The application includes CSRF protection for all POST requests

## Deployment

For production deployment:

1. Set `DEBUG = False` in `settings.py`
2. Configure proper ALLOWED_HOSTS
3. Use environment variables for all secrets
4. Set up a production web server (nginx, Apache)
5. Use a production WSGI server (Gunicorn, uWSGI)
6. Configure SSL/HTTPS
7. Set up proper logging and monitoring

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

Created as a Django web application for S3 file management.

## Acknowledgments

- Built with Django framework
- Uses boto3 for AWS S3 integration
- Styled with Bootstrap 5
- Icons from Font Awesome