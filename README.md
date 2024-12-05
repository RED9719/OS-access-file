# OS-access-file (python file_detail.py filename)
import os
import stat
import sys
import time

def file_details(file_name):
    print(f"Checking file: {file_name}")  # Debug statement
    try:
        # Get file status
        file_stat = os.stat(file_name)
        
        # File access time
        access_time = time.ctime(file_stat.st_atime)
        
        # File permissions
        permissions = stat.filemode(file_stat.st_mode)
        
        # File owner (user ID)
        owner_id = file_stat.st_uid
        
        # Print file details
        print(f"File: {file_name}")
        print(f"Access Time: {access_time}")
        print(f"Permissions: {permissions}")
        print(f"Owner ID: {owner_id}")

    except FileNotFoundError:
        print(f"The file {file_name} does not exist.")
    except PermissionError:
        print(f"Permission denied to access the file {file_name}.")
    except Exception as e:
        print(f"An error occurred: {e}")

def main():
    if len(sys.argv) != 2:
        print("Usage: python file_details.py <file_name>")
        return

    file_name = sys.argv[1]
    print(f"Received argument: {file_name}")  # Debug statement
    file_details(file_name)

if __name__ == "__main__":
    main()
