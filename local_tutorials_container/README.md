# Installation and building image (first time setup)
## Step 1: Install Prerequisites

Ensure you have the following installed on your computer:
- Docker Desktop: The application that runs and manages containers. Installation command on different OS can be found [here](https://docs.docker.com/get-docker/).

- VS Code (Recommended): For a better debugging and development.

- VS Code Dev Containers Extension: Essential for running VS Code inside the Docker environment. Install it from the VS Code...


## Step 2: Prepare Files and Build the Image
- Navigate to the `tut4` directory in your terminal.
- Build the Docker image using the following command:
  ```bash
  docker build -t tut4-multi-agent .
    ```
    tut4-multi-agent is the name of the image you are creating. You can choose any name you prefer.

## Step 3: Run the Container using VS Code Dev Containers
- Open VS Code from the folder `tut4`.
- VS Code will detect the Dockerfile and prompt you to "Reopen in Container." Click this button (or use the Command Palette → Dev Containers: Reopen in Container).
- Choose the "add configuration to workspace" option.
- Do not select any additional features when prompted.
- Do not any optional files or directories when prompted.

- The container will now build. When prompted choose to open the folder in the container.

## Step 4: start the assignment 
You can now open tut4_multi_agent.ipynb and start working. The environment is fully configured, and your progress is saved to your local folder.


# Once the setup is complete 
Everytime you open the folder in VS Code, it will ask if you want to reopen in the container. Click "Reopen in Container" to start working in the Docker environment.