# Action Repo

This repository is a dummy repository used to trigger GitHub Webhook events for the `webhook-repo` application.

## How to Trigger Events

1.  **Create a Repository on GitHub**
    - Create a new repository named `action-repo`.
    - Do not initialize with README (or do, it doesn't matter much, but empty is easier to push to).

2.  **Configure Webhooks**
    - Go to **Settings** > **Webhooks**.
    - Click **Add webhook**.
    - **Payload URL**: The URL where your `webhook-repo` app is running (e.g., `https://your-ngrok-url.io/webhook`).
    - **Content type**: `application/json`.
    - **Secret**: (Optional) If you set a SECRET_KEY in your `.env`, add it here (though the current implementation doesn't strictly validate signature for simplicity requests, it's good practice).
    - **Which events would you like to trigger this webhook?**: Select **Let me select individual events**.
        - Check **Pushes**.
        - Check **Pull requests**.
    - Click **Add webhook**.

3.  **Trigger `PUSH` Event**
    - Make a change to a file.
    - Commit and push:
      ```bash
      git add .
      git commit -m "Update README"
      git push origin main
      ```

4.  **Trigger `PULL_REQUEST` Event**
    - Create a new branch:
      ```bash
      git checkout -b feature-branch
      ```
    - Make changes and commit.
    - Push the branch:
      ```bash
      git push origin feature-branch
      ```
    - Go to GitHub and open a Pull Request from `feature-branch` to `main`.

5.  **Trigger `MERGE` Event**
    - In the Pull Request created above, click **Merge pull request**.
    - Confirm merge.

The `webhook-repo` application should receive these events and display them on the dashboard.
