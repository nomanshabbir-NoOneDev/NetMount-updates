# 🔑 Your own Google Drive keys: step by step

[← All guides](README.md)

**What this is for:** NetMount normally signs in to Google through rclone's own shared app. Everybody who uses rclone shares that app's request allowance, which is why you can see **"rate limit"** errors, and rclone has announced that the shared app will stop working during 2026. With **your own keys** the allowance is yours alone.

| | |
|---|---|
| ⏱️ **Time** | About 10 to 15 minutes, **once** |
| 💸 **Cost** | Free. No card needed |
| 🧰 **You need** | Any Google account and a web browser. A computer is easiest. A phone works too: open the links in Chrome and turn on **Desktop site** |
| 📱 **NetMount** | Version 1.7 or newer (Beta channel for now) |

**At the end you will have two pieces of text**, and you will paste them into NetMount:

- **Client ID**, which looks like `123456789012-abcdefg.apps.googleusercontent.com`
- **Client secret**, which looks like `GOCSPX-AbCdEf...`

> [!TIP]
> Keep this page open in one window and Google's console in another, and follow the numbers. Words in **bold** are the exact buttons or menu names you click. If Google has renamed a button slightly, pick the closest one.

---

## 📱 How to move around (read this first, especially on a phone)

From Part 3 on, you work in **Google Auth Platform**. It has its own menu with these pages: **Overview, Branding, Audience, Clients, Data Access**.

- **On a computer** this menu is always on the left.
- **On a phone it is hidden.** To open it, tap the small **shield-with-a-key icon** just under the black Google Cloud bar, at the left of the words *Google Auth Platform*.

  > [!WARNING]
  > Do **not** tap the **☰** (three lines) at the very top left. That is a different menu, for Google Cloud in general, and it does not list these pages.

- **Easier still:** every part below has a direct link. Tap the link and you land on the right page. Just make sure `NetMount` is the project selected at the top.

| Page | Direct link |
|---|---|
| Overview | <https://console.cloud.google.com/auth/overview> |
| Branding | <https://console.cloud.google.com/auth/branding> |
| Audience | <https://console.cloud.google.com/auth/audience> |
| Data Access | <https://console.cloud.google.com/auth/scopes> |
| Clients | <https://console.cloud.google.com/auth/clients> |

---

## Part 1: Make a project (1 minute)

A "project" is just a folder where Google keeps your keys.

1. Open **<https://console.cloud.google.com/>** and sign in with any Google account. It does **not** have to be the account that owns your Drive files.
2. The first time, Google asks you to accept the terms. Choose your country, tick the box and press **Agree and continue**.
3. At the top left, next to the **Google Cloud** logo, click the **project box**. It says **Select a project** or shows a project name.
4. In the window that opens, press **New project**.
5. **Project name:** type `NetMount`. Leave the rest as it is and press **Create**.
6. Wait about 10 seconds. Click **Select project** in the pop-up that appears (or choose `NetMount` in the project box again).

✅ **Check:** the top bar now shows **NetMount**. Every later step must be done with `NetMount` selected there.

---

## Part 2: Turn on the Google Drive API (1 minute)

1. Open **<https://console.cloud.google.com/apis/library/drive.googleapis.com>**
2. Press the blue **Enable** button and wait a few seconds.

✅ **Check:** the page now shows **API enabled** with a green tick.

> [!WARNING]
> Google now shows a message like *"To use this API, you may need credentials"* with a **Create credentials** button. **Do not press it.** It starts an older, confusing wizard. The next parts do it the easy way.

---

## Part 3: Set up the "consent screen" (3 minutes)

This is the page Google shows when you sign in. Google needs it before it will give you keys.

1. Open **<https://console.cloud.google.com/auth/overview>**
   (Google calls this the **Google Auth Platform**.)
2. Press **Get started**.
3. **Step 1, App information:**
   - **App name:** `NetMount`
   - **User support email:** choose your own e-mail from the list
   - Press **Next**.
4. **Step 2, Audience:** choose **External**, then press **Next**.
   *(If this is a school or work Google Workspace account you may be offered **Internal**. That also works, and then you can skip Parts 7 and 8.)*
5. **Step 3, Contact information:** type your e-mail address and press **Next**.
6. **Step 4, Finish:** tick **I agree to the Google API Services: User Data Policy**, then press **Continue**, then **Create**.

✅ **Check:** on a computer you see a menu on the left with **Overview, Branding, Audience, Clients, Data Access**. On a phone, tap the **shield-with-a-key icon** under the Google Cloud bar to open it (see *How to move around* above).

---

## Part 4: Allow the Drive permission (2 minutes)

1. Open **Data Access**: <https://console.cloud.google.com/auth/scopes> (or the menu, see *How to move around*).
2. Press **Add or remove scopes**.
3. A panel slides in from the right. Scroll to the bottom to the box **Manually add scopes**. Paste these three lines into it:

   ```
   https://www.googleapis.com/auth/drive
   https://www.googleapis.com/auth/drive.metadata.readonly
   https://www.googleapis.com/auth/docs
   ```

4. Press **Add to table**, then press **Update** at the bottom of the panel.
5. Press **Save** at the bottom of the page.

✅ **Check:** the page lists the three permissions. The main one reads *See, edit, create and delete all of your Google Drive files*.

---

## Part 5: Add yourself as a "test user" (1 minute)

1. Open **Audience**: <https://console.cloud.google.com/auth/audience> (or the menu).
2. Scroll to **Test users** and press **+ Add users**.
3. Type the Google address that **owns the Drive files** you want in NetMount, and press **Save**.
   Add every account you want to use.

---

## Part 6: Create the keys (2 minutes)

1. Open **Clients**: <https://console.cloud.google.com/auth/clients> (or the menu), then press **+ Create client**.
   *(Or on **Overview**, press **Create OAuth client**.)*
2. **Application type:** choose **Desktop app**.

   > [!IMPORTANT]
   > It must be **Desktop app**, not *Web application*. The wrong type gives the error `redirect_uri_mismatch` later.

3. **Name:** `NetMount`. Press **Create**.
4. A box **OAuth client created** appears with your **Client ID** and **Client secret**. Press the **copy** button beside each one and save them somewhere you can reach from your phone (send them to yourself in a message or a notes app).

> [!NOTE]
> Google may show the secret **only this once**. If you lose it, open the client under **Clients** and press **Add secret** to make a new one.

---

## Part 7: Finish the Branding page (3 minutes)

Google will not let you publish until this page is complete. If you open **Audience** first, **Publish app** is greyed out and says *"To publish your app, you must complete your configuration on the Branding page."* That is normal: do this part first.

1. Open **Branding**: <https://console.cloud.google.com/auth/branding> (or the menu).
2. **App information**
   - **App name:** `NetMount`
   - **User support email:** your own e-mail.
   - **App logo:** leave empty.
3. **App domain**: copy these exactly.
   - **Application home page:**

     ```
     https://github.com/nomanshabbir-NoOneDev/NetMount-updates
     ```

   - **Application privacy policy link:**

     ```
     https://github.com/nomanshabbir-NoOneDev/NetMount-updates#-permissions-and-privacy
     ```

   - **Application terms of service link:** leave empty.
4. **Authorized domains:** press **+ Add domain** and type:

   ```
   github.com
   ```

5. **Developer contact information:** type your e-mail address.
6. Press **Save** at the bottom of the page.

✅ **Check:** the page saves without a red message.

---

## Part 8: Publish the app. Do not skip this! (1 minute)

An app in **Testing** makes Google sign you out of Drive **every 7 days**. Publishing it stops that. It costs nothing and does not make your app public.

1. Open **Audience**: <https://console.cloud.google.com/auth/audience> (or the menu).
2. Under **Publishing status** it says **Testing**. Press **Publish app**. *(Still greyed out? Finish Part 7 first.)*
3. Read the box and press **Confirm**.

✅ **Check:** **Publishing status** now says **In production**.

*"Your app isn't verified" is normal here.* Google only asks for verification when an app is used by more than 100 people. You are the only user.

If you would rather not publish, you can stay in **Testing** and press **Sign in again** on your storages once a week.

---

## Part 9: Give the keys to NetMount (2 minutes)

1. Open NetMount: **Settings → Your own app keys → Google Drive**.
2. Turn the switch **on**.
3. Paste the **Client ID** and the **Client secret**, then press **Save**.
4. NetMount says *"Sign in again to your Google Drive storage"*. That is expected: a sign-in only works with the keys it was made with.
5. On the main screen, find each Google Drive storage. It says **Sign in needed**. Press **Sign in again**.
6. Your browser opens. Choose your Google account.
7. Google shows **"Google hasn't verified this app"**. This is your own app, so press **Advanced**, then **Go to NetMount (unsafe)**.
8. On **NetMount wants access to your Google Account**, **tick all the boxes** and press **Continue**.
9. When the page says it worked, go back to NetMount. The storage mounts again.

✅ **Check:** in **Settings → Your own app keys**, Google Drive says **Using your own keys**.

🎉 **Done.** You have your own allowance now.

---

## 🛠️ Something went wrong?

| What you see | What it means and what to do |
|---|---|
| `Error 400: redirect_uri_mismatch` | The key is not a **Desktop app**. Do Part 6 again, choose **Desktop app**, and paste the new keys |
| `Access blocked: ... has not completed the Google verification process` or `Error 403: access_denied` | Your Google address is not a test user and the app is still in Testing. Do Part 5 (add the address) or Part 8 (publish) |
| `Error 400: invalid_client` or *The OAuth client was not found* | The Client ID or secret was pasted wrongly. Copy them again from **Clients**, with no spaces before or after |
| Signed out again after about a week | The app is still in **Testing**. Do Part 8 |
| *Google Drive API has not been used in project ... or it is disabled* | Do Part 2 again, with the `NetMount` project selected in the top bar |
| **Publish app** is greyed out and says *complete your configuration on the Branding page* | Do Part 7 (Branding), save it, then try Part 8 again |
| I lost the secret | **Clients → NetMount → Add secret**, copy the new one, paste it in NetMount and press **Save** |
| Still "rate limit" sometimes | Normal at very heavy use. Keep **Gentle on request limits** switched on in the storage |

If you are stuck, open **Settings → Diagnostics** in NetMount, or the **Report a problem with this storage** button on the flipped card, and send the report to the NetMount group. It never contains your passwords, tokens or keys.

---

## ❓ Questions people ask

<details>
<summary><b>Is it really free? Do I need a card?</b></summary>

<br>

Yes, it is free. Creating a project, enabling the Drive API and making an OAuth client costs nothing and asks for no card.

</details>

<details>
<summary><b>Is it safe? What can the keys do?</b></summary>

<br>

The keys only tell Google *which app* is asking. They give nobody access to your files. Access needs your own sign-in as well. NetMount keeps the keys encrypted on your phone and leaves them out of exported storage lists. Still, do not post your **Client secret** in public.

</details>

<details>
<summary><b>Do I have to do this on every phone and for every Drive?</b></summary>

<br>

No. One set of keys works for any number of Drive storages and accounts. On another phone, paste the same two texts into **Settings → Your own app keys**.

</details>

<details>
<summary><b>How do I undo it?</b></summary>

<br>

Turn the switch off in **Settings → Your own app keys**. Your Drive storages then ask you to sign in again, and use rclone's shared keys. You can delete the `NetMount` project in the Google Cloud Console whenever you like.

</details>

<sub>Steps follow rclone's current instructions for making your own Google Drive client ID, written for NetMount. Google changes its console from time to time, so a button may be named a little differently.</sub>
