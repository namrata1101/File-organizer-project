# File-organizer-project
import os
import shutil
import time
import tkinter as tk
from tkinter import filedialog
from tkinter import ttk


def myPassantage(x):
    return x


# Define the function to organize files
def organize_files():
    passantage = 1

    # Get the source and destination directories from the user
    src_dir = filedialog.askdirectory(title='Select source directory')
    dst_dir = filedialog.askdirectory(title='Select destination directory')

    # Set the list of file extensions and their corresponding folders
    ext_folders = {
        '.TXT': 'text_files',
        '.PDF': 'pdf_files',
        '.JPG': 'image_files',
        '.PNG': 'image_files',
        '.GIF': 'image_files',
        '.MP3': 'audio_files',
        '.MP4': 'videos_files',
        '.RAR': 'zipped_files',
        '.ZIP': 'zipped_files'
    }

    # Create the destination folders if they don't already exist
    for folder_name in ext_folders.values():
        folder_path = os.path.join(dst_dir, folder_name)
        os.makedirs(folder_path, exist_ok=True)

    # Loop continuously to monitor for new files

    files = os.listdir(src_dir)
    print(len(files))

    # Loop through each file and move it to the appropriate folder
    for file_name in files:
        src_path = os.path.join(src_dir, file_name)

        # Check if the file is fully downloaded
        if os.path.isfile(src_path) and not file_name.endswith('.crdownload'):
            ext = os.path.splitext(file_name)[1].lower()
            folder_name = ext_folders.get(ext, 'other_files')
            folder_path = os.path.join(dst_dir, folder_name)

            # Create the destination folder if it doesn't exist
            os.makedirs(folder_path, exist_ok=True)

            # Move the file to the appropriate folder
            dst_path = os.path.join(folder_path, file_name)
            shutil.move(src_path, dst_path)

            print(f"Moved {file_name} to {folder_name} folder.")

        print(round((passantage / len(files)) * 100), "%")
        pd['value'] = myPassantage(round((passantage / len(files)) * 100))
        if pd['value'] == 100:
            myLabel = ttk.Label(root, text="Transfer complete..")
            myLabel.pack()
            break
        passantage += 1
        print(passantage)


# Create the GUI window
root = tk.Tk()
root.title('File Organizer')
root.geometry('400x300')
root.configure(bg='#F5F5F5')

style = ttk.Style()
style.configure('TButton', background='#4CAF50', foreground='white', font=('Arial', 12))
style.configure('TLabel', background='#F5F5F5', foreground='green', font=('Arial', 14, 'bold'))

# headings
myLabel = ttk.Label(root, text="nam systems")
myLabel.pack()

separate = ttk.Separator(root, orient='horizontal').pack(fill='x')

# progress bar
pd = ttk.Progressbar(root, orient='horizontal', length=395)
value_label = ttk.Label(root, text='transfering files..')
# place the bar
pd.pack()

# Create a button to organize files
organize_button = ttk.Button(root, text='Organize Files', command=organize_files)
organize_button.pack(pady=10)

# Start the GUI loop
root.mainloop()
