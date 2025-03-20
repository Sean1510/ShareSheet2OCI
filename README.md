# ShareSheet2OCI
Here's a step-by-step guide to create an iOS Shortcut that uploads content from the Share Sheet to Oracle Cloud Infrastructure (OCI) Object Storage using a Pre-Authenticated Request (PAR):

# Step 1: Create a Pre-Authenticated Request (PAR) in OCI
1. Navigate to your OCI Bucket:

    Open the OCI Console.
    
    Go to Storage > Buckets and select your target bucket.

2. Generate a PAR:

    Click Create Pre-Authenticated Request.
    
    Name: Give it a name (e.g., "PAR-Uploader-iOS").
    
    Access Type: Select Permit object writes (PUT).
    
    Object Name: Leave empty and check Allow any object with the prefix.
    
    Prefix: Enter uploads/ (or a custom path).
    
    Set an expiration time (e.g., 1 year).
    
    Click Create and Copy the PAR URL (e.g., https://namespace.compat.objectstorage.region.oraclecloud.com/n/namespace/b/bucket/o/uploads/).
   
    ![image](https://github.com/user-attachments/assets/c2ae7462-58fd-4422-8c7c-9fa06709d520)






# Step 2: Build the iOS Shortcut
Create a New Shortcut:

Open the Shortcuts app, tap +, and name it (e.g., "Upload to OCI").

Configure Share Sheet Access:

Tap the settings (ⓘ) and enable Show in Share Sheet.

Choose supported content types (e.g., files, images).

Add Shortcut Actions:

Get File Details (to extract the filename):

Copy
Get Details of [Input] → Name
URL-Encode the Filename:

Copy
URL Encode [Name]
Build the Full PAR URL:

Copy
Text: [PAR_BASE_URL][Encoded Filename]
Example: https://.../uploads/MyFile.jpg
Convert Input to File Content:

Copy
Get Contents of [Input]
Upload via PUT Request:

Copy
Contents of File → Headers:
  Content-Type: [Leave blank for auto-detection]
Method: PUT
URL: [Constructed PAR URL]
Full Shortcut Code
plaintext
Copy
1. Receive [Input] from Share Sheet
2. Get Details of [Input] → Name
3. URL Encode [Name]
4. Text: [PAR_BASE_URL][Encoded Filename]
5. Get Contents of [Input]
6. URL: [Constructed URL from Step 4]
7. Headers:
   - Content-Type: (Optional, auto-detected if blank)
8. Method: PUT
9. Show Result (Optional)
Testing
Share a file (e.g., photo) and select the Shortcut.

Verify the file appears in your OCI bucket under uploads/[filename].

Troubleshooting
403 Error: Check PAR expiration or permissions.

404 Error: Ensure the PAR URL includes the correct prefix.

Encoding Issues: Use URL Encode to handle special characters.

This method avoids complex API signing by leveraging OCI’s pre-signed URLs.
