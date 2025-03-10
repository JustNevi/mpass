# mpass - Simple Password Manager

Based on [pass](https://www.passwordstore.org/).

A command-line password manager that uses GPG encryption to securely store your passwords.

## Installation

### Windows

1. Install GPG4Win

   - Download GPG4Win from https://www.gpg4win.org/
   - Run the installer and follow the installation steps
   - During installation, make sure to select at least "GnuPG" component

2. Install Python Requirements

   ```bash
   pip install -r requirements.txt
   ```

3. Set up Environment Variables

   - Copy the `mpass` and `mpass.bat` files to a directory (e.g., `C:\Tools\mpass\`)
   - Add the directory to your PATH environment variable:
     1. Open System Properties (Win + Pause/Break or right-click Computer > Properties)
     2. Click "Advanced system settings"
     3. Click "Environment Variables"
     4. Under "System variables", find and select "Path"
     5. Click "Edit"
     6. Click "New"
     7. Add the path to your mpass directory (e.g., `C:\Tools\mpass\`)
     8. Click "OK" on all windows

4. Edit mpass.bat
   - Open mpass.bat in a text editor
   - Replace `C:\your\path\to\mpass` with the actual path to your mpass script
   - Save the file

## Usage

1. Initialize Password Store

   ```bash
   mpass init your.email@example.com
   ```

   Replace `your.email@example.com` with the email associated with your GPG key.

2. Get Store Information

   a. Display the GPG key used for the current password store:

   ```bash
   mpass info .
   ```

   b. Display the GPG key for a password store in a specific directory (absolute or relative path):

   ```bash
   mpass info /absolute/path/to/password-store
   # or
   mpass info ../relative/path/to/password-store
   ```

   c. Retrieve the password stored under "info" category:

   ```bash
   mpass info
   ```

3. Insert a Password

   You can insert a password in several ways:

   a. Interactive mode:

   ```bash
   mpass insert category/password-name
   ```

   You will be prompted to enter and confirm the password.

   b. Interactive multiline input:

   ```bash
   mpass insert category/password-name -m
   ```

   When using interactive multiline input, type each line of your content and press Enter.
   To finish entering content, press Enter on an empty line.

   c. From a file (multiline):

   ```bash
   type file.txt | mpass insert category/password-name -m
   ```

   d. Generate a password:

   ```bash
   mpass insert category/password-name -g
   ```

   e. Generate a password and display it:

   ```bash
   mpass insert category/password-name -G
   ```

   f. Force overwrite without confirmation:

   ```bash
   mpass insert category/password-name -f
   ```

4. Retrieve a Password

   a. Display password:

   ```bash
   mpass category/password-name
   ```

   b. Copy to clipboard (clears after 45 seconds):

   - Copy first line only:

   ```bash
   mpass category/password-name -c
   ```

   - Copy entire content:

   ```bash
   mpass category/password-name -C
   ```

5. Remove a Password

   ```bash
   mpass remove category/password-name
   ```

6. List All Passwords

   ```bash
   mpass list
   ```

7. Git Commands

   You can run git commands within the password store directory:

   ```bash
   mpass git status
   mpass git log
   ```

## Password Store Structure

Passwords are stored in the `.password-store` directory in your current working directory. Each password is stored in an encrypted `.gpg` file, organized in directories as specified in the path when inserting passwords.

For example:

```
.password-store/
    gmail/
        password-name.gpg
    work/
        password-name.gpg
```

## Security

mpass uses GPG encryption to secure your passwords. Your GPG key is used to encrypt and decrypt the passwords.
