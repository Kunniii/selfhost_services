# Self hosted services using Docker and Docker Compose

## What is this

This is my own Docker for self-hosted services since 200 BC. Now I an gonna public it on my GitHub.

It will save time for me, if next time, i have to set up my new OS and need to run these services.

Everyone can clone and use it! Here is how to setup this Docker Compose repo.

## How to use

Follow these steps to set up the project:

1. Copy the `.env.sample` file provided in the repository to create a new `.env` file using the following command:

    ```bash
    cp .env.sample .env
    ```

2. Edit the `.env` file with your own information. This file contains environment variables used by the application. Make sure to fill in all the required information.

3. Edit the `hosts` file on your computer. The `hosts` file is a plain text file used by the operating system to map hostnames to IP addresses. This file is used to redirect requests for a particular domain name to a specific IP address.

    * <b>On Windows</b>  
       The `hosts` file is located at `C:\Windows\System32\drivers\etc\hosts`

    * <b>On macOS and Linux</b>  
     The `hosts` file is located at `/etc/hosts`. To edit this file, you need to open it in a text editor with sudo privileges.

     Once you have located the `hosts` file, add the content from the `hosts` file provided in this repo.

4. Start the services

    Run the following command to start the application:

    ```bash
    docker compose up -d
    ```

## Use this repo as a Service (on Linux)

Create a file at `/etc/systemd/system/` named `selfhost.service`

Copy the content below. Remember to edit the `[FULL_PATH_TO_THIS_REPO]` and `[YOUR_USERNAME]` to match your system.

```yaml
[Unit]
Description=Self-hosted services

[Service]
User=[YOUR_USERNAME or `root`]
WorkingDirectory=[FULL_PATH_TO_THIS_REPO]
ExecStart=docker compose up -d

[Install]
WantedBy=multi-user.target
```

Save the file. Then start the service.

```sh
sudo systemctl start selfhost.service # or start [filename].service
```

Enable the service so that everytime you login to the computer, the services is always running.

```sh
sudo systemctl enable selfhost.service # or enable [filename].service
```
