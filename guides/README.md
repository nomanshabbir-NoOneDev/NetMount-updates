# 📚 NetMount guides

[← Back to NetMount](../README.md)

## 🔑 Your own app keys (fewer "rate limit" errors)

Google Drive, Dropbox and OneDrive count requests **per app**, and NetMount normally signs in through rclone's own app, which every rclone user shares. When its allowance runs out you get "rate limit" errors. Making a free app of your own gives you an allowance that is yours alone. It takes about 10 minutes, once.

| Service | Guide | Time |
|---|---|---|
| 🟢 **Google Drive** | [Your own Google Drive keys](google-drive.md) | about 10 to 15 minutes |
| 🔵 **Dropbox** | [Your own Dropbox keys](dropbox.md) | about 5 minutes |
| 🟦 **Microsoft OneDrive** | [Your own OneDrive keys](onedrive.md) | about 10 minutes |

Each guide lists every click, says what you should see after each part, and ends with a table of the errors people meet and how to fix them. Then you paste the two keys into **NetMount → Settings → Your own app keys**.

> [!TIP]
> Not sure you need this? Start with the **Gentle on request limits** switch in the storage (on by default). Your own keys are the lasting fix.
