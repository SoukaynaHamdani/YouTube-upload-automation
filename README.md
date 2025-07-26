# YouTube-upload-automation
# Automated YouTube Video Uploader & Playlist Manager

![n8n](https://img.shields.io/badge/n8n-Workflow-blueviolet )
![YouTube](https://img.shields.io/badge/Service-YouTube-red )
![Status](https://img.shields.io/badge/Status-Active-brightgreen )

This repository contains an [n8n](https://n8n.io/ ) workflow designed to automate the process of uploading videos to YouTube and organizing them into a new, dedicated playlist. It streamlines content management by handling video reading, playlist creation, video upload, and playlist population in a single, automated sequence.

## The Problem

Manually uploading a series of videos to YouTube can be a tedious and time-consuming process. For each video, one must:
1.  Navigate the YouTube Studio interface.
2.  Upload the video file.
3.  Set the title, description, and privacy status.
4.  Create a new playlist for the content series.
5.  Manually add the uploaded video to that playlist.

This workflow automates this entire sequence, saving significant time and reducing the chance of manual error.

## Workflow Breakdown

This workflow is triggered manually and executes the following steps in a coordinated manner:

1.  **Start (Manual Trigger):** The workflow begins when the user manually initiates it.

2.  **Parallel Execution:**
    *   **Create Playlist:** A new, private YouTube playlist is created immediately. The name is pre-defined in the node (e.g., "My Playlist Test").
    *   **Read Video Files:** Simultaneously, the workflow reads all video files from a specified local directory (`/home/soukaynaham/Videos/test`). It processes each video file it finds.

3.  **Upload Video:** For each video file read from the directory, this node performs the upload to YouTube.
    *   It dynamically sets the video's title using the original filename (`{{$binary.data.fileName}}`).
    *   It sets a default description and privacy status (e.g., "private").

4.  **Add to Playlist:** Once a video is successfully uploaded, this final node takes action.
    *   It retrieves the `playlistId` from the "Create Playlist" node.
    *   It retrieves the `videoId` from the "Upload Video" node.
    *   It adds the newly uploaded video to the newly created playlist, completing the sequence.

## Key Features & Benefits

*   **Automation:** Eliminates the manual, multi-step process of uploading and organizing YouTube videos.
*   **Efficiency:** Uploads multiple videos from a folder and creates their corresponding playlist in one run.
*   **Dynamic Titling:** Automatically uses the video's filename as the YouTube title, ensuring consistency.
*   **Error Reduction:** Reduces the risk of forgetting to add a video to a playlist or making typos in titles.
*   **Scalability:** Can be easily adapted to handle any number of videos placed in the target folder.

## Setup and Configuration

To use this workflow in your own n8n instance, follow these steps:

1.  **Import the Workflow:**
    *   Download the `.json` file from this repository.
    *   In your n8n canvas, select `File` > `Import from File...` and choose the downloaded JSON file.

2.  **Configure Credentials:**
    *   The workflow requires YouTube API access. You will need to create and connect your own YouTube OAuth2 credentials in n8n.
    *   Open the **"Create Playlist"**, **"Upload Video"**, and **"Add to Playlist"** nodes.
    *   In the "Credentials" section of each node, select your configured YouTube OAuth2 API credentials from the dropdown menu.

3.  **Update the File Path:**
    *   Open the **"Read Video"** node.
    *   Change the `Path` parameter from `/home/soukaynaham/Videos/test` to the absolute path of the folder on your local machine where your videos are stored.

4.  **Customize Parameters (Optional):**
    *   **Create Playlist Node:** Change the `Title` parameter to your desired playlist name.
    *   **Upload Video Node:** Modify the `Description` and `Privacy Status` as needed.

5.  **Activate and Run:**
    *   Save the workflow.
    *   Click the "Execute Workflow" button to run it manually.

Your videos will be uploaded and organized into the new playlist on your YouTube channel.
