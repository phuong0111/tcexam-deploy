# Offline Portable USB Deployment Guide for TCExam

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

This guide will walk you through creating a "plug-and-run" USB stick that will launch the TCExam application on any Windows computer without requiring administrator privileges, internet access, or software installation.

## Prerequisites

- A USB Flash Drive (at least 2GB of free space recommended).
- A computer with internet access (to download the necessary files initially).
- Your existing TCExam source code that you cloned earlier.

---

### Step 1: Download XAMPP Portable

We will use XAMPP Portable because it completely encapsulates Apache (web server), PHP, and MySQL (database server) into a single folder that can run from a USB drive.

1.  On your computer with internet access, go to the official Apache Friends download page for XAMPP Windows: [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
2.  Look for a version with PHP 8.2 (Since TCExam is tested and modern, 8.2 is recommended).
3.  Click on "More Downloads".
4.  Navigate to `XAMPP Windows` > The version you chose (e.g., `8.2.12`).
5.  Download the **`.zip`** or **`.7z`** portable version (e.g., `xampp-portable-windows-x64-8.2.12-0-VS16.zip`). **Do NOT download the `.exe` installer.**

### Step 2: Extract to USB Drive

1.  Plug your USB stick into your computer.
2.  Extract the downloaded `xampp-portable...zip` file directly to the root of your USB drive (so you have a folder like `E:\xampp`).

### Step 3: Run the Setup Script

For portable XAMPP to configure its internal paths correctly on whichever drive letter it's assigned to:

1.  Open the `xampp` folder on your USB drive.
2.  Double-click **`setup_xampp.bat`**.
3.  A command prompt will briefly appear, updating configuration files. Press enter when it prompts you to finish.

### Step 4: Copy TCExam Source Code

Now we need to place the application code inside XAMPP's web directory.

1.  Navigate to the `htdocs` directory within your XAMPP installation on the USB (`E:\xampp\htdocs`).
2.  Delete any existing files in `htdocs` (like `index.php` or `dashboard` folder) to keep things clean.
3.  Copy the `tcexam` folder (the one inside the `source_code` directory of this repository) into `htdocs`.
4.  Your path should look like this: `E:\xampp\htdocs\tcexam`.

### Step 5: Start the Servers

1.  Go back to the root of the `xampp` folder (`E:\xampp`).
2.  Double-click **`xampp-control.exe`**.
3.  The control panel will appear. Click **Start** next to **Apache** and **Start** next to **MySQL**.
    _(If Windows Firewall prompts you, click "Allow access")._

### Step 6: Create the Database

Now we need to set up the MySQL database that TCExam will use.

1.  Open a web browser and go to: `http://localhost/phpmyadmin`
2.  Click on the **"Databases"** tab at the top.
3.  In the "Create database" field, type: `TCExam`
4.  Choose `utf8mb4_unicode_ci` from the collation dropdown next to it.
5.  Click **Create**.

### Step 7: Import TCExam Database Structure

TCExam comes with SQL files that need to be imported to set up tables.

1.  In `phpMyAdmin`, make sure the new `TCExam` database is selected on the left sidebar.
2.  Click the **"Import"** tab at the top.
3.  Click **"Choose File"**.
4.  Navigate to your USB drive: `E:\xampp\htdocs\tcexam\install` and select `mysql_db_structure.sql`.
5.  Scroll to the bottom and click **"Import"**.
6.  Once successful, click the **"Import"** tab again, click **"Choose File"**, and this time select `db_data.sql` (also in the `install` folder).
7.  Click **"Import"**.

### Step 8: Configure TCExam to Connect to the Database

XAMPP's default MySQL root user has **no password**. We need to tell TCExam this.

1.  On your USB drive, navigate to `E:\xampp\htdocs\tcexam\shared\config`.
2.  Open **`tce_db_config.php`** with a text editor (like Notepad).
3.  Find the lines for the database connection and make sure they look exactly like this:
    ```php
    define('K_DATABASE_TYPE', 'MYSQL');
    define('K_DATABASE_HOST', 'localhost');
    define('K_DATABASE_PORT', '3306');
    define('K_DATABASE_NAME', 'TCExam');
    define('K_DATABASE_USER_NAME', 'root');
    define('K_DATABASE_USER_PASSWORD', ''); // Leave this empty for default XAMPP
    define('K_TABLE_PREFIX', 'tce_');
    ```
4.  Save and close the file.

### Step 9: Configure TCExam Main Path

We need to ensure the main path in TCExam is set properly.

1.  In the same folder `E:\xampp\htdocs\tcexam\shared\config`, open **`tce_paths.php`** with a text editor.
2.  Find the line for `K_PATH_MAIN` and change it to the following:
    ```php
    define('K_PATH_MAIN', 'E:\\xampp\\htdocs\\tcexam\\');
    ```
3.  Save and close the file.

### Step 10: Launch the Application!

Everything is set up. To run it:

1.  Open any web browser.
2.  Navigate to: `http://localhost/tcexam`
3.  You should see the TCExam interface.
4.  To access the admin panel, go to `http://localhost/tcexam/admin/code/` and log in with default credentials (Username: `admin`, Password: `1234`).

---

### How to use this on the Target Offline Windows Machine:

1.  Safely eject the USB drive from your current computer.
2.  Plug it into the target offline Windows machine.
3.  Open the USB drive, open the `xampp` folder.
4.  Launch `xampp-control.exe` and start **Apache** and **MySQL**.
5.  Open a web browser and go to `http://localhost/tcexam`.
6.  _When finished:_ Stop the servers in the control panel before unplugging the USB.
