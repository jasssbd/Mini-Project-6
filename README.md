# Mini-Project-6
ADVANCE PYTHON
import random
import string

# Generate 1000 lines of random strings
num_lines = 1000
string_length = 10  # Length of each random string

random_strings = [
    ''.join(random.choices(string.ascii_letters + string.digits, k=string_length))
    for _ in range(num_lines)
]

# Create the file content
file_content = '\n'.join(random_strings)

# Save to a text file
file_name = "random_strings_1000.txt"
with open(file_name, "w") as file:
    file.write(file_content)

print(f"File '{file_name}' created with 1000 lines of random strings.")
import random
import string

target_size = 5 * 1024 * 1024  # 5 MB in bytes
file_name = "random_5mb.txt"

def random_line(length=80):
    return ''.join(random.choices(string.ascii_letters + string.digits, k=length)) + '\n'

with open(file_name, 'w') as f:
    total_size = 0
    while total_size < target_size:
        line = random_line()
        f.write(line)
        total_size += len(line.encode('utf-8'))  # measure size in bytes

print(f"File '{file_name}' created with size approximately {total_size / (1024 * 1024):.2f} MB.")
import random
import string
import os

def generate_random_line(length=80):
    return ''.join(random.choices(string.ascii_letters + string.digits, k=length)) + '\n'

def generate_file(file_path, target_size_bytes):
    with open(file_path, 'w') as f:
        total_size = 0
        while total_size < target_size_bytes:
            line = generate_random_line()
            f.write(line)
            total_size += len(line.encode('utf-8'))

# Settings
num_files = 10
target_size = 5 * 1024 * 1024  # 5 MB in bytes

# Create 10 files
for i in range(1, num_files + 1):
    filename = f"random_file_{i}.txt"
    generate_file(filename, target_size)
    print(f"Created {filename}")
import random
import string
import os

def generate_random_line(length=100):
    return ''.join(random.choices(string.ascii_letters + string.digits, k=length)) + '\n'

def generate_large_file(filename, target_size_bytes):
    with open(filename, 'w') as f:
        total_size = 0
        while total_size < target_size_bytes:
            line = generate_random_line()
            f.write(line)
            total_size += len(line.encode('utf-8'))  # count bytes accurately
    print(f"Created {filename} ({total_size / (1024**3):.2f} GB)")

# Define sizes in GB
sizes_in_gb = [1, 2, 3, 4, 5]

# Generate files
for size in sizes_in_gb:
    filename = f"random_file_{size}GB.txt"
    target_size = size * 1024 * 1024 * 1024  # Convert GB to bytes
    generate_large_file(filename, target_size)
#!/bin/bash

# Loop through all files created in Q4
for size in 1 2 3 4 5; do
  echo "Converting file_${size}GB.txt to uppercase ..."
  awk '{ print toupper($0) }' file_${size}GB.txt > file_${size}GB_UPPER.txt
done
#!/bin/bash

# Q6: Convert all files to uppercase using parallel
export -f convert_upper

convert_upper() {
  local file=$1
  echo "Converting $file to uppercase ..."
  awk '{ print toupper($0) }' "$file" > "${file%.txt}_UPPER.txt"
}
# Q7
from google_images_download import google_images_download

def download_cat_images():
    response = google_images_download.googleimagesdownload()
    arguments = {"keywords": "cat", "limit": 10, "print_urls": False}
    paths = response.download(arguments)
    print("Downloaded images:", paths)

download_cat_images()
# Q8
from pytube import Search, YouTube

def download_ml_videos():
    search = Search("Machine Learning")
    for video in search.results[:10]:
        yt = YouTube(video.watch_url)
        stream = yt.streams.filter(progressive=True, file_extension='mp4').order_by('resolution').desc().first()
        print(f"Downloading: {yt.title}")
        stream.download(output_path="ml_videos")

download_ml_videos()

export -f convert_upper

ls file_*GB.txt | parallel convert_upper {}

