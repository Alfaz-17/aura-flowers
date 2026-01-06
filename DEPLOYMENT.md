# How to Deploy to Vercel

## 1. Prerequisites
Before deploying, ensure you have the following ready:
- A [Vercel Account](https://vercel.com/signup).
- Your project pushed to a GitHub repository (recommended) OR the Vercel CLI installed.
- Your database connection string (MongoDB URI).
- Your Cloudinary credentials.
- Your NextAuth secret.

## 2. Environment Variables
You will need to add the following environment variables to your Vercel project settings:

| Variable Name | Description |
| :--- | :--- |
| `MONGODB_URI` | Your MongoDB connection string. |
| `NEXTAUTH_SECRET` | A standard 32-character secret string (generate one with `openssl rand -base64 32` or just a long random string). |
| `NEXTAUTH_URL` | Set this to your Vercel domain (e.g., `https://your-project.vercel.app`). **Note:** Vercel automatically sets this for preview deployments, but you should set it for production. |
| `NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME` | Your Cloudinary cloud name. |
| `NEXT_PUBLIC_CLOUDINARY_API_KEY` | Your Cloudinary API key. |
| `CLOUDINARY_API_SECRET` | Your Cloudinary API secret. |

## 3. Deploy via GitHub (Recommended)
1.  **Push your code to GitHub**:
    ```bash
    git add .
    git commit -m "Ready for deploy"
    git push origin main
    ```
2.  **Go to Vercel Dashboard**: Click "Add New..." -> "Project".
3.  **Import Git Repository**: Select your `Aura-Flowners` repo.
4.  **Configure Project**:
    - **Framework Preset**: Next.js (should be auto-detected).
    - **Root Directory**: `my-app` (IMPORTANT: Since your app is in a subdirectory, you MUST set this).
    - **Environment Variables**: Expand this section and add all the variables listed above.
5.  **Deploy**: Click "Deploy". Vercel will build your app and verify everything works.

## 4. Deploy via CLI (Optional)
If you prefer not to use GitHub, you can deploy directly from your terminal:
1.  Install Vercel CLI: `npm i -g vercel`
2.  Run deploy command:
    ```bash
    cd my-app
    vercel
    ```
3.  Follow the prompts. When asked "Link to existing project?", say No (unless you already made one).
4.  For "In which directory is your code located?", standard `./` is fine if you are already in `my-app`.
5.  **Environment Variables**: You will still need to go to the Vercel Dashboard for this project to add your secrets (`MONGODB_URI`, etc.) for the site to function correctly.

## 5. Post-Deployment
- **Admin User**: The script `scripts/set-admin-user.ts` ran locally to set your admin user in your *local* database. If your Vercel app uses a *cloud* database (like MongoDB Atlas), you will need to run the seed script locally *pointed at your production DB* to create the admin user there, OR manually create the user in your production database.
- **Testing**: Visit your new URL and check the console for any errors.

> [!IMPORTANT]
> **Root Directory**: Since your project structure is `Aura-Flowners/my-app`, make sure Vercel knows the root is `my-app`. If you import the `Aura-Flowners` repo, set the "Root Directory" to `my-app` in the Vercel project settings.
