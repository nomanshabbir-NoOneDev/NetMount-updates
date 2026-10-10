# 🔑 Your own Dropbox keys: step by step

[← All guides](README.md)

**What this is for:** NetMount normally signs in to Dropbox through rclone's shared app, so everybody who uses rclone shares one request allowance. When it runs out you see **"too many requests"** errors. With **your own keys** the allowance is yours alone.

| | |
|---|---|
| ⏱️ **Time** | About 5 minutes, **once** |
| 💸 **Cost** | Free. No card needed |
| 🧰 **You need** | Any Dropbox account and a web browser. A computer is easiest. A phone works too: open the link in Chrome and turn on **Desktop site** |
| 📱 **NetMount** | Version 1.7 or newer (Beta channel for now) |

**At the end you will have two pieces of text**, and you will paste them into NetMount:

- **App key**
- **App secret**

> [!TIP]
> Words in **bold** are the exact buttons or menu names you click. If Dropbox has renamed a button slightly, pick the closest one.

---

## Part 1: Create the app (2 minutes)

1. Open **<https://www.dropbox.com/developers/apps>** and sign in. It does **not** have to be the account whose files you want in NetMount.
2. Press **Create app**.
3. **Choose an API:** pick **Scoped access**. *(If you see **Dropbox API** instead, pick that.)*
4. **Choose the type of access you need:** pick **Full Dropbox**.
5. **Name your app:** type a name that is just yours, for example `NetMount-yourname`. App names are shared by everybody on Dropbox, so a plain `NetMount` or `rclone` may already be taken.
6. Press **Create app**.

✅ **Check:** you are on your new app's page, with the tabs **Settings, Permissions, Branding, Analytics**.

---

## Part 2: Allow the permissions (1 minute)

Do this **before** anything else, or the sign-in later will complain about missing permissions.

1. Open the **Permissions** tab.
2. Tick these boxes:
   - `account_info.read`
   - `files.metadata.read`
   - `files.metadata.write`
   - `files.content.read`
   - `files.content.write`
   - `sharing.write`
3. Press **Submit** at the bottom of the page.

✅ **Check:** a green message says the permissions were saved.

---

## Part 3: Add the sign-in address (1 minute)

1. Open the **Settings** tab.
2. Find **OAuth 2**, then **Redirect URIs**.
3. Type this exactly, with the slash at the end:

   ```
   http://localhost:53682/
   ```

4. Press **Add**.

✅ **Check:** the address now appears in a list under the box.

---

## Part 4: Copy your keys (1 minute)

1. Stay on the **Settings** tab. Near the top you see **App key**: copy it.
2. Next to it is **App secret**, hidden. Press **Show**, then copy it.
3. Save both somewhere you can reach from your phone (send them to yourself in a message or a notes app).

---

## Part 5: Give the keys to NetMount (2 minutes)

1. Open NetMount: **Settings → Your own app keys → Dropbox**.
2. Turn the switch **on**.
3. Paste the **App key** and the **App secret**, then press **Save**.
4. NetMount says *"Sign in again to your Dropbox storage"*. That is expected: a sign-in only works with the keys it was made with.
5. On the main screen, find each Dropbox storage. It says **Sign in needed**. Press **Sign in again**.
6. Your browser opens. Sign in to Dropbox if asked, then press **Continue** and **Allow**.
7. When the page says it worked, go back to NetMount. The storage mounts again.

✅ **Check:** in **Settings → Your own app keys**, Dropbox says **Using your own keys**.

🎉 **Done.** You have your own allowance now.

---

## 🛠️ Something went wrong?

| What you see | What it means and what to do |
|---|---|
| `redirect_uri` error or *Invalid redirect URI* | The address from Part 3 is missing or has a typo. It must be exactly `http://localhost:53682/` and you must have pressed **Add** |
| *Your app is missing permissions* or `missing_scope` | Do Part 2 again, press **Submit**, then press **Sign in again** in NetMount |
| *App key not found* or `invalid_client` | The App key or secret was pasted wrongly. Copy both again, with no spaces before or after |
| *That app name is already taken* | Choose another name in Part 1, for example with your own name added |
| Still "too many requests" sometimes | Normal at very heavy use. Keep **Gentle on request limits** switched on in the storage |

If you are stuck, open **Settings → Diagnostics** in NetMount, or the **Report a problem with this storage** button on the flipped card, and send the report to the NetMount group. It never contains your passwords, tokens or keys.

---

## ❓ Questions people ask

<details>
<summary><b>Is it really free? Do I need a card?</b></summary>

<br>

Yes, it is free. Creating an app in the Dropbox App Console costs nothing and asks for no card.

</details>

<details>
<summary><b>Is it safe? What can the keys do?</b></summary>

<br>

The keys only tell Dropbox *which app* is asking. They give nobody access to your files. Access needs your own sign-in as well. NetMount keeps the keys encrypted on your phone and leaves them out of exported storage lists. Still, do not post your **App secret** in public.

</details>

<details>
<summary><b>Do I have to do this for every Dropbox storage?</b></summary>

<br>

No. One set of keys works for any number of Dropbox storages. On another phone, paste the same two texts into **Settings → Your own app keys**.

</details>

<details>
<summary><b>How do I undo it?</b></summary>

<br>

Turn the switch off in **Settings → Your own app keys**. Your Dropbox storages then ask you to sign in again, and use rclone's shared keys. You can delete the app in the App Console whenever you like.

</details>

<sub>Steps follow rclone's current instructions for making your own Dropbox app, written for NetMount. Dropbox changes its console from time to time, so a button may be named a little differently.</sub>
