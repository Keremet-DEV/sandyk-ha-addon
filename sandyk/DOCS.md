# Sandyk

Backup of photos, videos and files from phones to your Home Assistant, a duplicate finder,
and space freed on the phone. Phones at home connect directly; from outside — through a relay,
no public IP needed.

## Getting started

1. Start the add-on and open its **Log** tab. Until the server has an account it writes a setup
   code there, like `ABCD-EFGH`.
2. Open the web UI (**Open web UI**) and create an account with that code. This first account
   is the admin. Registration then closes unless **Open registration** is on; the admin adds
   people in **Settings → Users**. (You can create the first account from the phone app instead:
   it asks for the same code.)
3. In the phone app: **Settings → Connect a Server → Own Server**, address
   `http://<Home Assistant address>:8080`, and sign in.
4. To reach the server away from home without a public IP: in the app, **Settings → Access
   from the internet**, pick a name and get `https://<name>.sandyk.cloud`. It needs a Sandyk
   account (sign in with Apple or Google).

Step-by-step instructions for every way to install: https://sandyk.app/server/

## Options

- **Where to keep files** (`storage_dir`): photos, videos and files, by default
  `/share/sandyk`. An external drive works: mount it in **Settings → System → Storage**
  and point this to `/media/<drive>/sandyk`. Moving it later: stop the add-on, move the
  `blobs` folder, change the option, start.
- **Home addresses** (`local_urls`): left empty, the add-on announces the host's addresses with
  the published port, so phones at home skip the relay.
- **Relay** (`relay_url`, `relay_token`): only for a relay of your own or a name issued by hand.
  For `<name>.sandyk.cloud` leave them empty and take the name in the app (step 4 above). The
  relay only forwards encrypted traffic; the certificate belongs to your server.
- **Days in trash** (`trash_days`), **Log level** (`log_level`).

## Backups

The database (accounts, folders, albums) lives in the add-on's data and is in Home Assistant
backups; the server also keeps 7 daily snapshots of it. The files in `storage_dir` are in a
backup only if the backup includes that folder (`share` or `media`) — a photo library may be
too big for that; keep a copy of the folder elsewhere instead.
