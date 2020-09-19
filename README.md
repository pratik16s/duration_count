# duration_count
count the  run time duration of a folder....
import os
import moviepy.editor
import tkinter as tk
from tkinter import simpledialog
def count_time(str1):
    global video_duration
# Create an object by passing the list's element as a string
    video = moviepy.editor.VideoFileClip(str1)
# Contains the duration of the video in terms of seconds
    video_duration = int(video.duration)
    return video_duration
# Converts into more readable format
def convert(seconds):
    hours = seconds // 3600
    seconds %= 3600
    mins = seconds // 60
    seconds %= 60
    return hours, mins, seconds
if __name__ == '__main__':
    files = []
    i = 0
    root = tk.Tk()
    root.withdraw()
    # the input dialog
    path= simpledialog.askstring(title="Test",
                                      prompt="enter your path:")

    # path = str(input("Enter the name of your text file - please use / backslash when typing in directory path: "))
    # r=root, d=directories & f= files

    for r, d, f in os.walk(path):
        for file in f:
            if '.mp4' in file:
                files.append(os.path.join(r, file))
                i += 1
            if '.mkv' in file:
                files.append(os.path.join(r, file))
                i += 1
    # folder contains all these mp4 files
    for f in files:
        print(f)
Total_video_duration=0
for l in range(i):
    str1=files[l]
    count_time(str1)
    Total_video_duration=Total_video_duration+video_duration
hours, mins, secs = convert(Total_video_duration)
print(f"total time taken to play all mp4 & mkv files in: {hours}:{mins}:{secs}")

