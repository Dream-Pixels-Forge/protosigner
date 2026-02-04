# Protosigner Extension for Qwen CLI

The Protosigner extension bridges the Qwen CLI and the Stitch MCP (Model Context Protocol) server, allowing you to manage design projects using natural language. Streamline your workflow in Stitch—Google’s AI-powered UI/UX tool—by controlling assets and code generation directly from your terminal.

<img width="1115" height="560" alt="terminal" src="https://github.com/user-attachments/assets/0303c0c7-ef32-4168-88f9-0539af3532b3" />


<img width="1480" height="913" alt="stich_protosigner" src="https://github.com/user-attachments/assets/887880a1-9641-4f52-8761-49138f6c915c" />


## ✨ Features

- **🎨 List Projects:** View a list of your Stitch projects.
- **🎨 Project Details:** Get detailed information about a specific project.
- **🎨 Retrieve Screens:** Access all screens within a given project.
- **🎨 Download Assets:** Download assets such as images and HTML files.
- **🎨 Generate Screen From Text:** Generate new screens from text prompt, using Gemini 3 Pro or Gemini 3 Flash(default) models.
- **🎨 More features coming soon...**

## 📋 Prerequisites

Before using this extension, ensure you have the following installed:

1. **Qwen CLI:**
    - Install the Qwen CLI

    - Refer to [Qwen CLI Documentation](https://github.com/QwenLM/qwen-code) for installation instructions.

2. **gcloud CLI:**
    - Install and initialize the [gcloud CLI](https://cloud.google.com/sdk/docs/install).
    - Ensure you have a Google Cloud Project to use with Stitch.

## 🚀 Installation

Run the following command in your terminal to install the Stitch extension:

```bash
qwen extensions install https://github.com/Dream-Pixels-Forge/protosigner --auto-update
```

## 🔐 Configuration & Authentication

To use the Stitch extension, you need to configure authentication. The Stitch MCP server supports two authentication methods:

- **API Key Authentication**: Simpler to set up. Use an API key generated from Stitch settings, powered by Google Cloud Managed Projects. Ideal for personal use and quick setup.
- **Application Default Credentials (ADC)**: Uses Google Cloud credentials for authentication. Requires your own Google Cloud project with proper IAM permissions, needs multiple manual steps to set up.

Choose one method below based on your needs.

### 1. Authenticate with Auth API Key

1. **Get API Key:**
    - Go to [Stitch](https://stitch.withgoogle.com/).
    - Click on your profile icon in the top-right corner.
    - Select "Stitch Settings" from the dropdown menu.
    - Go to the "API Keys" section.
    - Click on "Create Key".
    - Copy the generated API key.

2. **Configure Extension:**
    Run the following commands to configure your API key (replace `your-api-key-here` with your actual API key):

    ```bash
    export API_KEY="your-api-key-here"
    sed "s/YOUR_API_KEY/$API_KEY/g" ~/.qwen/extensions/protosigner/gemini-extension-apikey.json > ~/.qwen/extensions/protosigner/gemini-extension.json
    ```

### 2. Authenticate with Application Default Credentials (ADC)

1. **Login to gcloud:**

    ```bash
    gcloud auth login
    ```

2. **Configure Project and Quota:**
    Set your project ID variable and configure the project. Replace `your-project-id` with your actual Google Cloud Project ID.

    ```bash
    export PROJECT_ID="your-project-id"
    gcloud config set project $PROJECT_ID
    gcloud auth application-default set-quota-project $PROJECT_ID
    ```

3. **Enable Stitch MCP API:**
    Enable the Stitch MCP service on your project.

    ```bash
    gcloud beta services mcp enable stitch.googleapis.com --project=$PROJECT_ID
    ```

4. **Grant Permissions:**
    Your account needs the `roles/serviceusage.serviceUsageConsumer` role.

    ```bash
    gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member="user:your-email@gmail.com" \
      --role="roles/serviceusage.serviceUsageConsumer"
    ```

5. **Login to ADC:**

    ```bash
    gcloud auth application-default login
    ```

6. **Configure Extension:**
    Run the following command to update the configuration file with your project ID:

    ```bash
    sed "s/YOUR_PROJECT_ID/$PROJECT_ID/g" ~/.qwen/extensions/protosigner/gemini-extension-adc.json > ~/.qwen/extensions/protosigner/gemini-extension.json
    ```

## 💡 Usage

1. **Start Qwen CLI:**
    Launch the Qwen CLI
 with the Stitch extension enabled:

    ```bash
    qwen
    ```

2. **List Available Tools:**
    To see all available MCP tools, including those from Stitch, use:

    ```
    /mcp list

    /mcp desc
    ```

3. **Interact with Stitch:**
    Use the `/stitch` command prefix to send natural language requests. Examples:

    - **List Projects:**

        ```
        /stitch What Stitch projects do I have?
        ```

    - **Get Project Details:**

        ```
        /stitch Tell me details about my project 6677573127824787033
        ```

    - **List Screens:**

        ```
        /stitch Give me all the screens of project 6677573127824787033
        ```

    - **Download Assets:**

        ```
        /stitch Download the image of screen 7393b8177be0490f89eb8f2c1e4cfb37
        /stitch Download the HTML of screen 7393b8177be0490f89eb8f2c1e4cfb37
        ```

    - **Generate new Screens:**

        You can generate new screens from text prompt, using Qwen3, Gemini 3 Pro or Gemini 3 Flash (default) models.

        ```
        /stitch Design a mobile app for people who love skiing in the Alps, using Gemini 3 Pro.
        ```

    - **Enhance a Prompt:**

        ```
        /stitch Enhance this prompt: "Design a landing page for a podcast about the latest in Design and AI."
        ```

## 💸 Pricing

- Stitch MCP is **free of charge**.

## 🔧 Resources

- [Stitch](https://stitch.withgoogle.com/): The official Stitch web application.
- [Qwen CLI Extensions](https://github.com/QwenLM/qwen-code): Documentation on using extensions in Qwen CLI.
- [GitHub Issues](https://github.com/Dream-Pixels-Forge/protosigner/issues): Report bugs or request new features.

## 📄 Legal

Your use of the Stitch API is governed by the Google Terms and Use Policy, and the Google APIs Terms, and your Stitch settings. The Stitch Privacy Notice describes how your data is handled.

- **[Google Terms and Use Policy](https://policies.google.com/terms)**
- **[Google APIs Terms of Service](https://console.cloud.google.com/tos?id=universal)**
- **[Stitch Privacy Notice](https://stitch.withgoogle.com/privacy)**
- **[Apache License 2.0](https://github.com/Dream-Pixels-Forge/protosigner/blob/main/LICENSE)**
