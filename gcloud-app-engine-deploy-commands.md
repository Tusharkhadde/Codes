# Google App Engine Deployment: Successful Commands

Project: `local-businesss-support-system` (App Engine app already existed, region `asia-south1`)
Account: `tusharkhadde06@gmail.com` (Editor role)

> Note: Editor access cannot run `gcloud app create`. It was not needed, because the app already existed. Editor is enough to deploy.

## 1. Go to the project folder

```powershell
cd C:\Users\mayur\tushar\Project\hello-api
```

## 2. Log in to gcloud

```powershell
gcloud auth login
```

## 3. List projects and find the project ID

Use the project **ID**, not the project name.

```powershell
gcloud projects list
```

## 4. Set the active project

General form (replace `YOUR_PROJECT_ID` with the real project ID, not the name):

```powershell
gcloud config set project YOUR_PROJECT_ID
```

For this project:

```powershell
gcloud config set project local-businesss-support-system
gcloud config get-value project
```

## 5. Enable the required APIs

```powershell
gcloud services enable appengine.googleapis.com cloudbuild.googleapis.com
```

## 6. Check that the App Engine app exists

```powershell
gcloud app describe --project=local-businesss-support-system
```

Expected: `servingStatus: SERVING` and `locationId: asia-south1`.

## 7. Deploy the code

An `app.yaml` must be present in the folder.

```powershell
gcloud app deploy --project=local-businesss-support-system
```

Type `y` when prompted: `Do you want to continue (Y/n)?`

Result:

```
Deployed service [default] to [https://local-businesss-support-system.el.r.appspot.com]
```

## 8. Open the deployed app

```powershell
gcloud app browse
```

## 9. View logs (optional)

```powershell
gcloud app logs tail -s default
```

## Redeploy after code changes

```powershell
cd C:\Users\mayur\tushar\Project\hello-api
gcloud app deploy --project=local-businesss-support-system
```

## Stop the app

`gcloud app update --serving-status` does not work in this gcloud version. Use the Console:

1. Open `https://console.cloud.google.com/appengine?project=local-businesss-support-system`
2. Go to **Settings**
3. Click **Disable application** and type the project ID to confirm

Needs Owner or App Engine Admin rights. To turn it back on, use **Enable application** on the same page.

## Troubleshooting

| Problem | Fix |
|---|---|
| `appengine.applications.create` denied | Editor cannot create the app. Ask the project Owner to create it, or deploy to an app that already exists. |
| `does not have permission to access projects instance [hello-api]` | You used the project name. Use the project ID instead. |
| Active project resets | Run `gcloud config set project <PROJECT_ID>`, or add `--project=<PROJECT_ID>` to every command. |
| Typed a command at the `(Y/n)` prompt | Enter only `y` or `n` at that prompt. |
