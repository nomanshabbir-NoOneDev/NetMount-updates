# 🔑 Your own Microsoft OneDrive keys: step by step

[← All guides](README.md)

**What this is for:** NetMount normally signs in to OneDrive through rclone's shared app, so everybody who uses rclone shares one request allowance. When it runs out you see **"throttled"** or **"activityLimitReached"** errors. With **your own keys** the allowance is yours alone.

| | |
|---|---|
| ⏱️ **Time** | About 10 minutes, **once** |
| 💸 **Cost** | Free. Microsoft may ask for a phone number or a card to **verify** a new account. It is not charged |
| 🧰 **You need** | A Microsoft account (the one you use for OneDrive is fine) and a web browser. A computer is easiest. A phone works too: open the links in Chrome and turn on **Desktop site** |
| 📱 **NetMount** | Version 1.7 or newer (Beta channel for now) |

**At the end you will have two pieces of text**, and you will paste them into NetMount:

- **Application (client) ID**, which looks like `0123abcd-1234-5678-9abc-def012345678`
- **Client secret value**, a long text with letters, numbers and `~`

> [!TIP]
> Words in **bold** are the exact buttons or menu names you click. If Microsoft has renamed a button slightly, pick the closest one.

---

## Part 1: Open the app registrations (2 minutes)

1. Open **<https://entra.microsoft.com/>** and sign in with your Microsoft account.
   *(The older address <https://portal.azure.com/> works too: search for **App registrations** at the top.)*
2. If Microsoft says you have no directory or subscription, follow its **Sign up** or **Start free** offer. Creating the free account is needed once. Registering an app costs nothing.
3. In the left menu open **Entra ID** (or **Identity**), then **App registrations**.

✅ **Check:** you see a page titled **App registrations** with a **+ New registration** button.

---

## Part 2: Register the app (2 minutes)

1. Press **+ New registration**.
2. **Name:** `NetMount`.
3. **Supported account types:** choose the third option:
   **Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts**
4. **Redirect URI (optional):**
   - In the first box choose **Web**.
   - In the second box **type** this, with the slash at the end (type it, do not paste it):

     ```
     http://localhost:53682/
     ```

5. Press **Register**.
6. On the page that opens, find **Application (client) ID** and copy it. Save it somewhere you can reach from your phone.

---

## Part 3: Make a secret (2 minutes)

1. In the left menu click **Certificates & secrets**.
2. Under **Client secrets** press **+ New client secret**.
3. **Description:** `NetMount`. **Expires:** choose **24 months**. Press **Add**.
4. In the list, look at the column **Value** and press the **copy** button beside it.

   > [!IMPORTANT]
   > Copy the **Value**, **not** the *Secret ID*. The Value is shown **only now**. If you leave the page without copying it, make a new secret.

5. Save it together with the Client ID.

> [!NOTE]
> A secret stops working after the time you chose. Put a reminder in your calendar. When it expires NetMount shows **Sign in needed**: make a new secret and paste it into **Settings → Your own app keys**.

---

## Part 4: Allow the permissions (2 minutes)

1. In the left menu click **API permissions**.
2. Press **+ Add a permission**, choose **Microsoft Graph**, then **Delegated permissions**.
3. Use the search box to find and tick each of these:
   - `Files.Read`
   - `Files.ReadWrite`
   - `Files.Read.All`
   - `Files.ReadWrite.All`
   - `offline_access`
   - `User.Read`
   - `Sites.Read.All` *(only needed if you want SharePoint libraries; skip it if Microsoft will not allow it)*
4. Press **Add permissions**.

✅ **Check:** the list shows all of them with the type **Delegated**.

*(With a school or work account, your administrator may have to approve some of them. If the sign-in later says **Need admin approval**, ask them to press **Grant admin consent** here.)*

---

## Part 5: Give the keys to NetMount (2 minutes)

1. Open NetMount: **Settings → Your own app keys → Microsoft OneDrive**.
2. Turn the switch **on**.
3. Paste the **Application (client) ID** and the **Client secret value**, then press **Save**.
4. NetMount says *"Sign in again to your OneDrive storage"*. That is expected: a sign-in only works with the keys it was made with.
5. On the main screen, find each OneDrive storage. It says **Sign in needed**. Press **Sign in again**.
6. Your browser opens. Choose your Microsoft account and, when it asks, press **Accept** (or **Yes**).
7. When the page says it worked, go back to NetMount. The storage mounts again.

✅ **Check:** in **Settings → Your own app keys**, Microsoft OneDrive says **Using your own keys**.

🎉 **Done.** You have your own allowance now.

---

## 🛠️ Something went wrong?

| What you see | What it means and what to do |
|---|---|
| `AADSTS50011` *The redirect URI does not match* | The address in Part 2 is wrong. Open your app, **Authentication**, and make sure there is a **Web** address exactly `http://localhost:53682/` |
| `AADSTS7000215` *Invalid client secret* | You copied the *Secret ID* instead of the **Value**. Make a new secret (Part 3) and paste its **Value** |
| `AADSTS700016` *Application not found in the directory* | Wrong **Supported account types**. Open your app, **Authentication**, and choose *…and personal Microsoft accounts* |
| `AADSTS65001` or *Need admin approval* | A work or school account needs its administrator to approve the permissions (Part 4) |
| `AADSTS7000222` *The client secret keys are expired* | Make a new secret (Part 3) and paste it into NetMount |
| Still "throttled" sometimes | Normal at very heavy use. Keep **Gentle on request limits** switched on in the storage |

If you are stuck, open **Settings → Diagnostics** in NetMount, or the **Report a problem with this storage** button on the flipped card, and send the report to the NetMount group. It never contains your passwords, tokens or keys.

---

## ❓ Questions people ask

<details>
<summary><b>Is it really free?</b></summary>

<br>

Yes. Registering an app costs nothing. Microsoft may want to verify a new account with a phone number or a card, and does not charge it.

</details>

<details>
<summary><b>Is it safe? What can the keys do?</b></summary>

<br>

The keys only tell Microsoft *which app* is asking. They give nobody access to your files. Access needs your own sign-in as well. NetMount keeps the keys encrypted on your phone and leaves them out of exported storage lists. Still, do not post your **secret** in public.

</details>

<details>
<summary><b>Do I have to do this for every OneDrive storage?</b></summary>

<br>

No. One set of keys works for any number of OneDrive storages, personal or work. On another phone, paste the same two texts into **Settings → Your own app keys**.

</details>

<details>
<summary><b>How do I undo it?</b></summary>

<br>

Turn the switch off in **Settings → Your own app keys**. Your OneDrive storages then ask you to sign in again, and use rclone's shared keys. You can delete the app registration whenever you like.

</details>

<sub>Steps follow rclone's current instructions for making your own OneDrive app, written for NetMount. Microsoft changes its portal from time to time, so a button may be named a little differently.</sub>
