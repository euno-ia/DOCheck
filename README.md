# DOCheck! — flat-folder Flask edition

Files are all in ONE folder: `index.html` (HTML+CSS+JS), `app.py` (all backend modules), `requirements.txt`, `.env.example`, `.gitignore`.

## Run locally

```bash
python -m pip install -r requirements.txt
python app.py
```
Visit http://127.0.0.1:5000. First launch generates a fresh `docheck.db` and prints one-time admin/staff credentials in the terminal. Change passwords before production use.

## GitHub hosting

GitHub Pages **cannot run this Flask application** and cannot store account data. Upload this repository to GitHub, then deploy the Flask service to a Python-capable hosting platform such as Render, Railway, or a VPS. Example start command: `gunicorn 'app:create_app()'`. Set `SECRET_KEY` as an environment variable. Configure persistent storage for `docheck.db` or migrate to a hosted PostgreSQL database before public use.

**Database**: For privacy, the source ZIP's SQLite database was NOT included: it contains 22 user accounts and checkup data. A new database is created automatically on first launch. The original demo doctor entries in the application are placeholders, not verified RHU Cantilan personnel. Verify and replace before public launch.

**Security**: Do not commit real patient records, `.secret`, or API keys. SQLite on ephemeral cloud disks loses records on restart/deploy. This version has NOT been fully security-audited or integration-tested.

## Architecture

`index.html` is served as both login and dashboard by Flask's template loader; it contains all original CSS and JS. Logos are embedded as base64 data URIs. `app.py` embeds the original Python modules and registers their Flask routes in memory. This is a packaging change, not a conversion to a GitHub Pages-compatible static application.
