# ShareSheet2OCI
Here's a step-by-step guide to create an iOS Shortcut that uploads content from the Share Sheet to Oracle Cloud Infrastructure (OCI) Object Storage using a Pre-Authenticated Request (PAR):

# Step 1: Create a Pre-Authenticated Request (PAR) in OCI
1. Navigate to your OCI Bucket:

    Open the OCI Console.
    
    Go to Storage > Buckets and select your target bucket.

2. Generate a PAR:

    Click Create Pre-Authenticated Request.
    
    **Name**: Give your project a memorable identity. In the screenshot below, I used "PAR-Uploader-iOS," but feel free to use the default name provided by OCI if you prefer.

    **Pre-Authenticated Request Target**: As depicted in the screenshot, I kept the default target as 'Bucket'.
    
    **Access Type**: While the default radio button selects "Permit object reads," I opted to switch it to "Permit object reads and writes" to allow more flexibility.
    
    **Enable Object Listing**: In the screenshot, you can see I enabled this option to show all objects.
    
    **Expiration**: Set this according to your needs; in my example, I've chosen December 31, 9999 for long-term access.
    
    Click Create and Copy the PAR URL.
   
    ![image](https://github.com/user-attachments/assets/c2ae7462-58fd-4422-8c7c-9fa06709d520)






# Step 2: Build the iOS Shortcut
1. Create a New Shortcut:

    Open the Shortcuts app, tap +, and name it (e.g., "ShareSheet2OCI").

2. Configure Share Sheet Access:

    Tap the settings (ⓘ) and enable Show in Share Sheet.

    Choose supported content types (e.g., files, images).

3. Add Shortcut Actions:

    1). Receive [Types of Content] from Share Sheet  
    2). **Repeat with Each**: Repeat with Each Item in [Shortcut Input]  
       └─ 3). **Get Details of Files**: Get [Detail -> Name] of [Repeat Item]
       └─ 4). **URL Encode**: URL Encode [Name]  
       └─ 5). **Text**: Text: [Your PAR_URL in Step 1][Select Variable -> URL Encoded Text] (there should be no space between the 2 parts)
       └─ 6). **Get Contents of URL**: Get Contents of [Text]: Method -> PUT; Request of URL -> File; File -> [Repeat Item] 
       └─ 7). **Show Notification**: (Optional) Text -> [Contents of URL]

    Please see below screenshot as an example:
    ![image](https://github.com/user-attachments/assets/50768da0-ea0e-4f7f-a174-1715e517730c)

    Feel free to copy directly from iCloud: https://www.icloud.com/shortcuts/c70bb1b234064b04bfa2969eb60a82d4

