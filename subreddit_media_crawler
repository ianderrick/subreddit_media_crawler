import requests
import os
import tkinter as tk
from tkinter import filedialog

# Function to download a file
def download_file(url, file_name):
  response = requests.get(url)
  open(file_name, "wb").write(response.content)

# Function to crawl a subreddit and download media
def crawl_subreddit(subreddit):
  # Make a request to the subreddit's JSON data
  headers = {'User-Agent': 'My Reddit Crawler'}
  response = requests.get(f'https://www.reddit.com/r/{subreddit}/.json', headers=headers)
  data = response.json()

  # Get the directory to save the files to
  root = tk.Tk()
  root.withdraw()
  save_directory = filedialog.askdirectory(parent=root, initialdir="/", title='Please select a directory to save the files to')

  # Iterate through the posts and download media
  for post in data['data']['children']:
    post_data = post['data']
    url = post_data['url']
    file_extension = os.path.splitext(url)[1]
    if file_extension in ['.jpg', '.png', '.gif', '.mp4']:
      file_name = f"{post_data['id']}{file_extension}"
      download_file(url, os.path.join(save_directory, file_name))

# Function to create the GUI
def create_gui():
  # Create the main window
  window = tk.Tk()
  window.title("Subreddit Crawler")

  # Create a label and text box for the subreddit name
  subreddit_label = tk.Label(text="Enter the subreddit name:")
  subreddit_label.pack()
  subreddit_entry = tk.Entry()
  subreddit_entry.pack()

  # Create a button to start the crawling process
  crawl_button = tk.Button(text="Crawl Subreddit", command=lambda: crawl_subreddit(subreddit_entry.get()))
  crawl_button.pack()

  # Run the GUI
  window.mainloop()

# Create the GUI
create_gui()
